# Laboratorio No. 03: Robótica Industrial - Manipulador EPSON T3-401S

## 1. Cuadro Comparativo de Manipuladores
| Característica | EPSON T3-401S | Motoman MH6 | ABB IRB 140 |
| :--- | :--- | :--- | :--- |
| **Carga Máxima** | 3 kg | 6 kg | 6 kg |
| **Alcance** | 400 mm | 1422 mm | 800 mm |
| **Grados de Libertad** | 4 ejes (SCARA) | 6 ejes | 6 ejes |
| **Velocidad Máxima** | J1-J2: 3700 mm/s, J3: 1000 mm/s, J4: 2600°/s | Hasta 1000°/s aprox. según eje | Hasta 200°/s según eje |
| **Aplicaciones Típicas** | Pick & place, ensamblaje de piezas pequeñas, manipulación veloz | Soldadura, empaquetado, cuidado de máquinas, manipulación | Ensamblaje, desbarbado, soldadura, cuidado de máquinas |


# 2. Configuraciones Iniciales (Home)

## Definición de Home

La posición Home corresponde a una posición de referencia segura utilizada para inicializar el robot, verificar la calibración y comenzar o finalizar rutinas de trabajo. Esta posición permite que el manipulador se ubique en una configuración conocida, reduciendo el riesgo de colisiones y facilitando la ejecución repetitiva de programas.

En EPSON RC+ 7.0, la posición Home puede configurarse como un punto enseñado (Teach Point) y posteriormente ser llamada desde cualquier programa mediante instrucciones de movimiento.

## Posición Articular

La posición Home utilizada:

| Articulación | Posición |
|-------------|-----------|
| J1 | 0° |
| J2 | 0° |
| J3 | 0 mm (posición superior) |
| J4 | 0° |


## Rangos de Movimiento

| Eje | Rango de Movimiento |
|------|-------------------|
| J1 | ±132° |
| J2 | ±141° |
| J3 | 150 mm |
| J4 | ±360° |

---



# 3. Operación Manual

## Modos de Movimiento

### Movimiento Articular (Joint)

El modo articular permite controlar individualmente cada eje del robot.

**Procedimiento:**

1. Colocar el robot en modo Teach.
2. Abrir la ventana **Jog & Teach** en EPSON RC+.
3. Seleccionar el modo **Joint**.
4. Mover cada articulación utilizando los controles de desplazamiento.

**Ejes disponibles:**

- J1 (+/-)
- J2 (+/-)
- J3 (+/-)
- J4 (+/-)

### Movimiento Cartesiano

El modo cartesiano permite desplazar directamente el TCP (*Tool Center Point*) en coordenadas espaciales.

#### Traslaciones

- X+
- X-
- Y+
- Y-
- Z+
- Z-

#### Rotación

- Rz+
- Rz-

Este modo resulta útil para posicionar el efector final respecto al entorno de trabajo.

## Control de Velocidad

### Niveles Disponibles

El robot permite ajustar la velocidad de operación mediante porcentaje o velocidad lineal.

| Parámetro | Rango |
|------------|---------|
| Speed | 1 – 100 % |
| SpeedS | 0.1 – 2000 mm/s |

### Cambio de Nivel

1. Abrir la ventana **Jog & Teach**.
2. Localizar el parámetro **Speed**.
3. Seleccionar el porcentaje deseado.
4. Confirmar el nuevo valor.

### Identificación del Nivel

El porcentaje de velocidad seleccionado se muestra directamente en la interfaz de EPSON RC+ 7.0.

---




## 4. Software y Entorno de Control
### EPSON RC+ 7.0
* **Funcionalidades:** [Describir aplicaciones principales]
* **Comunicación:** [Explicar cómo se conecta con el manipulador y procesa los comandos]

### Análisis Comparativo de Software
| Herramienta | Ventajas | Limitaciones | Usos Específicos |
| :--- | :--- | :--- | :--- |
| **EPSON RC+ 7.0** | | | |
| **RoboDK** | | | |
| **RobotStudio** | | | |

## 5. Diseño de Gripper Neumático
* **Esquema:** [Insertar imagen o diagrama]
* **Componentes:** [Lista de partes: ventosa, válvulas, tuberías, etc.]
* **Configuración E/S:** [Detallar conexión de las entradas/salidas digitales]

## 6. Trayectoria: Patrón de Caballo (Ajedrez)
* **Plano de planta:** [Insertar diagrama de la cubeta y posiciones iniciales]
* **Diagrama de flujo:** [Insertar flujo lógico de la rutina]
* **Código (EPSON RC+ 7.0):**
    ```basic
    ' Incluir aquí el partes importantes del código desarrollado
    ```

## 7. Evidencias
* **Simulación:** [Enlace al video de la simulación en EPSON RC+ 7.0]
* **Funcionamiento Gripper:** [Enlace al video del gripper levantando el huevo]
