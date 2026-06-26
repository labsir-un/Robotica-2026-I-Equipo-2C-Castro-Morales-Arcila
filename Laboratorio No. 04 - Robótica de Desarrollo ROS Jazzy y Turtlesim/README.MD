## Descripción General

Este laboratorio introduce los fundamentos de **ROS 2 Jazzy Jalisco** mediante el control del simulador Turtlesim. Se implementa un nodo propio en Python con `rclpy` llamado `control_tortuga`, el cual permite controlar `turtle1` de forma manual desde el teclado, ejecutar trayectorias automáticas, dibujar letras personalizadas y gestionar un sistema líder-seguidor con `turtle2` de manera simultánea, sin usar `turtle_teleop_key`.

## 1. Control Manual de la Tortuga

El nodo `control_tortuga` captura las entradas del teclado usando la función `leer_tecla()`, que opera en modo raw sobre `stdin` con un timeout de 50 ms. Los comandos de movimiento se publican directamente sobre `/turtle1/cmd_vel` sin bloquear la ejecución del nodo.

| Tecla | Acción |
|:-----:|--------|
| ↑ | Avanzar hacia adelante (`linear.x = 2.0`) |
| ↓ | Retroceder (`linear.x = -2.0`) |
| ← | Girar a la izquierda (`angular.z = 1.5`) |
| → | Girar a la derecha (`angular.z = -1.5`) |

<div align="center">
  <img src="./img/control_manual.png" alt="Control manual de la tortuga" width="600"/>
  <p><em>Figura 1. Control manual de turtle1 desde el teclado.</em></p>
</div>

## 2. Funciones Automáticas

Cada función automática se ejecuta en un hilo independiente (`threading.Thread`) para no bloquear el bucle principal del teclado. El método auxiliar `mover(lineal, angular, duracion)` controla el desplazamiento dividiendo la duración en pasos de 50 ms.

| Tecla | Función | Implementación |
|:-----:|---------|----------------|
| S | Cuadrado | 4 iteraciones: avanza 2 s → gira π/2 |
| T | Triángulo equilátero | 3 iteraciones: avanza 2 s → gira 2π/3 |
| R | Reiniciar posición | Teleport al centro (5.544, 5.544) |
| P | Activar / desactivar lápiz | Servicio `/turtle1/set_pen` |
| A | Trayectoria automática dentro de límites | Si x o y < 1.0 o > 10.0 → gira; si no → avanza con curvatura |
| Q | Detener movimiento | Publica `Twist()` con todo en 0 |
| L | Limpiar pantalla | Servicio `/clear` |

<div align="center">
  <img src="./img/trayectorias_auto.png" alt="Trayectorias automáticas" width="600"/>
  <p><em>Figura 2. Ejecución de figuras automáticas en Turtlesim.</em></p>
</div>


## 3. Dibujo de Letras Personalizadas

Las letras se implementaron como secuencias de movimientos lineales y angulares combinados, ejecutadas en hilos independientes. Cada letra corresponde a las iniciales de los integrantes del equipo.

| Tecla | Letra | Referencia |
|:-----:|-------|------------|
| M | M | [Marco] |
| D | D | Daniel |
| 1 | P | [Pablo] |

<div align="center">
  <img src="./img/letras.png" alt="Dibujo de letras personalizadas" width="600"/>
  <p><em>Figura 3. Trayectorias de letras personalizadas dibujadas por turtle1.</em></p>
</div>


## 4. Sistema Líder-Seguidor

`turtle2` se crea llamando al servicio `/spawn` mediante la tecla **K**, con posición inicial en (2.0, 2.0). Una vez creada, un timer a 10 Hz ejecuta el método `seguir()`, el cual calcula la distancia y el error angular entre ambas tortugas y publica comandos proporcionales sobre `/turtle2/cmd_vel` para que `turtle2` se aproxime progresivamente a `turtle1`.

```python
cmd.linear.x  = 1.5 * dist          # velocidad proporcional a la distancia
cmd.angular.z = 6.0 * error_angulo  # corrección proporcional del ángulo
```

El seguidor solo actúa cuando la distancia entre tortugas supera los 0.5 unidades, evitando oscilaciones cuando están muy cerca.

<div align="center">
  <img src="./img/lider_seguidor.png" alt="Sistema líder-seguidor" width="600"/>
  <p><em>Figura 4. Sistema líder-seguidor con turtle1 y turtle2 en Turtlesim.</em></p>
</div>


## 5. Arquitectura ROS 2

### Nodos, Tópicos y Servicios

El nodo `control_tortuga` concentra toda la lógica del sistema. Publica comandos de velocidad para ambas tortugas, se suscribe a sus posiciones y consume varios servicios de Turtlesim.

| Elemento | Nombre | Tipo | Descripción |
|----------|--------|------|-------------|
| Nodo | `/control_tortuga` | Nodo propio | Controla turtle1 y el seguidor de turtle2 |
| Tópico | `/turtle1/cmd_vel` | Publicador | Velocidad de turtle1 |
| Tópico | `/turtle2/cmd_vel` | Publicador | Velocidad de turtle2 (seguidor) |
| Tópico | `/turtle1/pose` | Suscriptor | Posición en tiempo real de turtle1 |
| Tópico | `/turtle2/pose` | Suscriptor | Posición en tiempo real de turtle2 |
| Servicio | `/spawn` | Cliente | Creación de turtle2 en el simulador |
| Servicio | `/turtle1/set_pen` | Cliente | Activar / desactivar el lápiz |
| Servicio | `/turtle1/teleport_absolute` | Cliente | Reinicio de posición de turtle1 |
| Servicio | `/reset` | Cliente | Reinicio completo del simulador |
| Servicio | `/clear` | Cliente | Limpieza de trazos en pantalla |

### Visualización con rqt_graph

**Nodes only** — muestra únicamente los nodos activos y las conexiones entre ellos a través de los tópicos. Se pueden identificar los dos nodos principales (`/control_tortuga` y `/turtlesim`) y los cuatro tópicos de comunicación.

<div align="center">
  <img src="./img/NodesOnly.jpg" alt="rqt_graph - Nodes only" width="700"/>
  <p><em>Figura 5. Vista Nodes only — arquitectura de comunicación entre nodos.</em></p>
</div>

**Nodes/Topics (active)** — muestra los nodos y únicamente los tópicos activos en ese momento. Se visualizan los namespaces de cada tortuga y los tópicos de posición y velocidad que están siendo usados en tiempo real.

<div align="center">
  <img src="./img/NodesTopicsActive.jpg" alt="rqt_graph - Nodes/Topics active" width="700"/>
  <p><em>Figura 6. Vista Nodes/Topics (active) — tópicos activos por namespace.</em></p>
</div>

**Nodes/Topics (all)** — muestra todos los tópicos disponibles, incluyendo los que no tienen suscriptores activos en ese instante. Útil para verificar que todos los tópicos del sistema están correctamente registrados.

<div align="center">
  <img src="./img/NodesTopicsAll.jpg" alt="rqt_graph - Nodes/Topics all" width="700"/>
  <p><em>Figura 7. Vista Nodes/Topics (all) — todos los tópicos registrados en el sistema.</em></p>
</div>

### Comandos de Inspección

**`ros2 node list`**  
Lista todos los nodos activos en el sistema. Permite verificar que `/control_tortuga` y `/turtlesim` están corriendo correctamente.

```bash
ros2 node list
```

<div align="center">
  <img src="./img/node_list.png" alt="ros2 node list" width="600"/>
</div>


**`ros2 topic list`**  
Muestra todos los tópicos disponibles en la red ROS 2, incluyendo los de posición y velocidad de ambas tortugas.

```bash
ros2 topic list
```

<div align="center">
  <img src="./img/topic_list.png" alt="ros2 topic list" width="600"/>
</div>

**`ros2 topic echo /turtle1/pose`**  
Muestra en tiempo real los mensajes publicados por `/turtlesim` sobre la posición de `turtle1`, con los campos `x`, `y`, `theta`, `linear_velocity` y `angular_velocity`.

```bash
ros2 topic echo /turtle1/pose
```

<div align="center">
  <img src="./img/topic_echo_pose.png" alt="ros2 topic echo /turtle1/pose" width="600"/>
</div>


**`ros2 topic info /turtle1/cmd_vel`**  
Devuelve el tipo de mensaje del tópico (`geometry_msgs/msg/Twist`), el número de publicadores y suscriptores activos. Confirma que el nodo está publicando correctamente.

```bash
ros2 topic info /turtle1/cmd_vel
```

<div align="center">
  <img src="./img/topic_info_cmdvel.png" alt="ros2 topic info /turtle1/cmd_vel" width="600"/>
</div>

**`ros2 service list`**  
Lista todos los servicios disponibles. Se identifican los servicios usados por el nodo: `/spawn`, `/turtle1/set_pen`, `/turtle1/teleport_absolute`, `/reset` y `/clear`.

```bash
ros2 service list
```

<div align="center">
  <img src="./img/service_list.png" alt="ros2 service list" width="600"/>
</div>


## 6. Diagrama de Flujo

## 7. Video Demostrativo

<div align="center">
  <a href="[URL_DEL_VIDEO]">
    <img src="https://img.youtube.com/vi/[VIDEO_ID]/hqdefault.jpg" alt="Video demostrativo - Lab 04 ROS 2 Turtlesim" width="600"/>
  </a>
  <p><em>Video demostrativo del laboratorio — ROS 2 Jazzy Jalisco, Turtlesim.</em></p>
</div>


## Referencias

- [LabSIR UN — Intro Linux Ubuntu 24.04](https://github.com/labsir-un/01_Rob_2026_I_Intro_Ubuntu_24.04.git)
- [LabSIR UN — Intro ROS 2 Jazzy Jalisco](https://github.com/labsir-un/02_Rob_2026_I_Intro_ROS2_Jazzy.git)
- [LabSIR UN — Intro Turtlesim ROS 2 Jazzy](https://github.com/labsir-un/03_Rob_2026_I_ROS2_Jazzy_Turtlesim.git)
- [LabSIR UN — Arquitectura ROS 2 Jazzy](https://github.com/labsir-un/04_Rob_2026_I_ROS2_Jazzy_Architecture.git)
- [ROS 2 Jazzy — Guía de instalación](https://docs.ros.org/en/jazzy/Installation.html)
- [ROS 2 Jazzy — Tutorial Turtlesim](https://docs.ros.org/en/jazzy/Tutorials/Beginner-CLI-Tools/Introducing-Turtlesim/Introducing-Turtlesim.html)
