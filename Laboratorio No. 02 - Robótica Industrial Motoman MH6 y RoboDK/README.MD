<div align="center">
  <picture>
    <source srcset="https://imgur.com/5bYAzsb.png" media="(prefers-color-scheme: dark)">
    <source srcset="https://imgur.com/Os03JoE.png" media="(prefers-color-scheme: light)">
    <img src="https://imgur.com/Os03JoE.png" alt="Escudo UNAL" width="350px">
  </picture>

  <h1>Laboratorio No. 02 Robótica Industrial - Análisis y Operación del Manipulador Motoman MH6.</h1>
</div>

---

## Solución planteada:

Para el desarrollo del segundo laboratorio de robótica industrial, se plantea el análisis y operación del manipulador **Motoman MH6**, tomando como referencia la experiencia obtenida previamente con el manipulador **ABB IRB140** en RobotStudio. En esta práctica se busca comprender las principales características técnicas del Motoman MH6, sus configuraciones iniciales, los modos de movimiento manual, los niveles de velocidad y el uso del software **RoboDK** para la simulación y ejecución de trayectorias.

Inicialmente, se realiza una comparación técnica entre el Motoman MH6 y el ABB IRB140, con el fin de identificar diferencias importantes en cuanto a alcance, carga útil, repetibilidad, velocidades articulares, aplicaciones típicas y software de programación. Posteriormente, se estudian las posiciones iniciales del Motoman, específicamente **Home 1** y **Home 2**, para comprender su utilidad dentro de una rutina de operación segura.

Una vez reconocidas las características del manipulador, se procede a describir los modos de movimiento manual, incluyendo el movimiento por articulaciones, el movimiento cartesiano, las traslaciones y las rotaciones respecto a los ejes del sistema de referencia. Además, se analiza el control de velocidad manual, ya que este aspecto es fundamental para realizar movimientos seguros durante la enseñanza de puntos y la validación de trayectorias.

Finalmente, se trabaja con el software **RoboDK**, el cual permite crear una estación virtual, simular trayectorias, generar programas y establecer una comunicación con el manipulador físico. En este laboratorio, la actividad principal consiste en diseñar una **trayectoria polar**, simularla en RoboDK y posteriormente ejecutarla en el manipulador Motoman MH6 comandado desde el computador.

---

## Comparación técnica entre el Motoman MH6 y el ABB IRB140

A continuación se presenta un cuadro comparativo entre el manipulador **Motoman MH6** y el **ABB IRB140**, considerando sus características técnicas principales.

| Característica | Motoman MH6 | ABB IRB140 |
|---|---|---|
| Fabricante | Yaskawa Motoman | ABB Robotics |
| Tipo de robot | Manipulador industrial articulado | Manipulador industrial articulado |
| Número de ejes | 6 ejes | 6 ejes |
| Carga útil máxima | 6 kg | 6 kg |
| Alcance máximo aproximado | 1422 mm | 810 mm |
| Repetibilidad | ±0.08 mm | ±0.03 mm |
| Masa aproximada | 130 kg | 98 kg |
| Montaje | Piso, pared o techo | Piso, pared o invertido |
| Controlador asociado | DX100 / controlador Motoman | IRC5 |
| Software trabajado | RoboDK | RobotStudio |
| Aplicaciones típicas | Manipulación, ensamble, empaque, dispensado, soldadura y atención de máquinas | Manipulación, ensamble, manufactura flexible, soldadura, limpieza, empaque y automatización industrial |

El **Motoman MH6** es un robot industrial de seis ejes, con una carga útil de **6 kg** y un alcance aproximado de **1422 mm**, lo que le permite cubrir una zona de trabajo amplia. Debido a su diseño compacto y su capacidad de movimiento, puede ser utilizado en aplicaciones de manipulación, ensamble, empaque, soldadura, dispensado y atención de máquinas.

Por otro lado, el **ABB IRB140** también es un robot industrial de seis ejes con una carga útil de **6 kg**, pero con un alcance menor, aproximadamente de **810 mm**. Esto lo hace más adecuado para estaciones compactas donde se requiere precisión y flexibilidad en espacios reducidos.

A partir de esta comparación, se puede observar que ambos manipuladores tienen la misma capacidad de carga nominal, pero el Motoman MH6 presenta una ventaja en cuanto a alcance, mientras que el ABB IRB140 se caracteriza por ser un robot más compacto y estar directamente integrado al ecosistema de programación de ABB mediante RobotStudio.

---

## Velocidades y rangos de movimiento del Motoman MH6

En el manipulador Motoman MH6, cada articulación posee un rango de movimiento y una velocidad máxima específica. Estos parámetros son importantes porque determinan la capacidad del robot para ejecutar movimientos rápidos, alcanzar distintas zonas del espacio de trabajo y evitar configuraciones no deseadas durante la programación.

| Eje | Velocidad máxima aproximada | Rango de movimiento aproximado |
|---|---|---|
| `S` | 220 °/s | ±170° |
| `L` | 200 °/s | +155° / -90° |
| `U` | 220 °/s | +250° / -175° |
| `R` | 410 °/s | ±180° |
| `B` | 410 °/s | +225° / -45° |
| `T` | 610 °/s | ±360° |

Los ejes `S`, `L` y `U` corresponden principalmente al posicionamiento general del brazo, mientras que los ejes `R`, `B` y `T` están asociados a la orientación de la muñeca y de la herramienta. Por esta razón, los últimos ejes suelen presentar velocidades mayores, ya que permiten ajustar rápidamente la orientación del efector final.

---

## Velocidades del ABB IRB140

Para el caso del ABB IRB140, las velocidades articulares aproximadas son las siguientes:

| Eje | Velocidad máxima aproximada |
|---|---|
| Eje 1 | 200 °/s |
| Eje 2 | 200 °/s |
| Eje 3 | 260 °/s |
| Eje 4 | 360 °/s |
| Eje 5 | 360 °/s |
| Eje 6 | 450 °/s |

Aunque el ABB IRB140 tiene menor alcance que el Motoman MH6, mantiene velocidades adecuadas para aplicaciones industriales compactas. Además, al trabajar con RobotStudio, el usuario puede simular el comportamiento del robot utilizando el controlador virtual de ABB, lo que permite validar rutinas antes de ejecutarlas físicamente.

---

## Análisis comparativo de los manipuladores

A partir de las características técnicas revisadas, se puede afirmar que ambos robots pertenecen a la categoría de manipuladores industriales de seis grados de libertad. Sin embargo, presentan diferencias importantes en su diseño y campo de aplicación.

El **Motoman MH6** resulta conveniente para tareas donde se requiere mayor alcance y una zona de trabajo más amplia. Esto puede ser útil en procesos de manipulación de piezas, empaque, soldadura o atención de máquinas. Su alcance de 1422 mm le permite cubrir distancias mayores sin necesidad de desplazar la base del robot.

El **ABB IRB140**, en cambio, es un robot más compacto. Su menor alcance puede ser una ventaja cuando se trabaja en celdas pequeñas o estaciones donde el espacio disponible es limitado. Además, su integración con RobotStudio permite trabajar de forma directa con el lenguaje RAPID y con el controlador virtual de ABB.

En términos generales, el Motoman MH6 ofrece mayor cobertura espacial, mientras que el ABB IRB140 ofrece una solución compacta y altamente integrada con el entorno ABB.

---

## Configuraciones iniciales del Motoman MH6

Durante la operación del manipulador Motoman MH6, se identifican configuraciones iniciales conocidas como **Home 1** y **Home 2**. Estas posiciones permiten ubicar el robot en una postura de referencia antes de iniciar una rutina, realizar una calibración visual o preparar el sistema para un movimiento seguro.

#### Configuración `Home 1`

La configuración **Home 1** corresponde a una posición inicial del manipulador en la cual sus articulaciones se ubican de forma ordenada y segura. Esta posición puede utilizarse como punto de partida para una rutina o como posición de reposo del robot.

| Articulación | Posición en Home 1 |
|---|---|
| `S` | `[PENDIENTE]` |
| `L` | `[PENDIENTE]` |
| `U` | `[PENDIENTE]` |
| `R` | `[PENDIENTE]` |
| `B` | `[PENDIENTE]` |
| `T` | `[PENDIENTE]` |

**`Imagen propuesta:`** Fotografía del manipulador Motoman MH6 ubicado en la configuración Home 1.

#### Configuración `Home 2`

La configuración **Home 2** corresponde a una segunda posición de referencia del manipulador. Esta puede ser utilizada para ubicar el robot en una postura alternativa, dependiendo de la rutina, la herramienta instalada o la zona de trabajo.

| Articulación | Posición en Home 2 |
|---|---|
| `S` | `[PENDIENTE]` |
| `L` | `[PENDIENTE]` |
| `U` | `[PENDIENTE]` |
| `R` | `[PENDIENTE]` |
| `B` | `[PENDIENTE]` |
| `T` | `[PENDIENTE]` |

**`Imagen propuesta:`** Fotografía del manipulador Motoman MH6 ubicado en la configuración Home 2.

#### Comparación entre `Home 1` y `Home 2`

La elección entre **Home 1** y **Home 2** depende de la finalidad de la operación. Si se busca una posición segura para iniciar o finalizar una rutina, será más conveniente la configuración que deje al manipulador alejado de obstáculos y con menor riesgo de colisión. Por otro lado, si se busca iniciar una trayectoria específica, será mejor la configuración que reduzca desplazamientos innecesarios y facilite el acceso al área de trabajo.

**`Nota:`** Esta sección debe completarse con las posiciones reales observadas en el laboratorio y con una justificación basada en la experiencia de operación del manipulador.

---

## Movimiento manual del manipulador Motoman MH6

Durante la práctica, el movimiento manual del manipulador Motoman MH6 permite al usuario desplazar el robot mediante el teach pendant. Este procedimiento es importante para enseñar puntos, verificar posiciones, ajustar trayectorias y comprobar que el robot pueda moverse sin colisionar con elementos de la estación.

El movimiento manual puede realizarse principalmente en dos formas:

- Movimiento por articulaciones.
- Movimiento cartesiano.

Además, dentro del movimiento cartesiano se pueden realizar:

- Traslaciones en los ejes `X`, `Y` y `Z`.
- Rotaciones alrededor de los ejes `X`, `Y` y `Z`.

#### Movimiento por articulaciones

En el modo de movimiento por articulaciones, cada eje del robot se controla de forma independiente. Esto permite modificar directamente la posición angular de las articulaciones `S`, `L`, `U`, `R`, `B` y `T`.

Este modo es útil cuando se requiere cambiar la postura general del robot, liberar una configuración incómoda, evitar una singularidad o ubicar el manipulador en una posición inicial antes de realizar movimientos más precisos.

**`Procedimiento pendiente:`**

1. `[PENDIENTE]` Encender o habilitar el teach pendant.
2. `[PENDIENTE]` Seleccionar el modo de movimiento por articulaciones.
3. `[PENDIENTE]` Seleccionar el eje o articulación que se desea mover.
4. `[PENDIENTE]` Usar las teclas correspondientes para mover la articulación en sentido positivo o negativo.
5. `[PENDIENTE]` Verificar en pantalla el cambio de posición angular.

**`Imagen propuesta:`** Pantalla del teach pendant durante el movimiento por articulaciones.

#### Movimiento cartesiano

En el modo cartesiano, el robot se mueve respecto a un sistema de coordenadas. En este caso, el usuario controla el desplazamiento del TCP de la herramienta en los ejes `X`, `Y` y `Z`, sin seleccionar directamente cada articulación.

Este modo resulta más intuitivo cuando se desea mover la herramienta en línea recta, aproximarla a una pieza o posicionarla sobre una superficie de trabajo.

**`Procedimiento pendiente:`**

1. `[PENDIENTE]` Seleccionar el modo de movimiento cartesiano.
2. `[PENDIENTE]` Verificar el sistema de referencia activo.
3. `[PENDIENTE]` Mover el TCP en los ejes `X`, `Y` y `Z`.
4. `[PENDIENTE]` Confirmar visualmente la dirección de movimiento.
5. `[PENDIENTE]` Ajustar la posición final de la herramienta.

**`Imagen propuesta:`** Pantalla del teach pendant durante el movimiento cartesiano.

#### Traslaciones en `X`, `Y` y `Z`

Las traslaciones permiten desplazar la herramienta de forma lineal sobre los ejes del sistema de referencia. Este procedimiento es útil para ubicar el TCP sobre puntos específicos de una trayectoria o para aproximar la herramienta a la superficie de trabajo.

- Movimiento en `X`: `[PENDIENTE]`
- Movimiento en `Y`: `[PENDIENTE]`
- Movimiento en `Z`: `[PENDIENTE]`

**`Imagen propuesta:`** Evidencia del manipulador realizando una traslación lineal.

#### Rotaciones alrededor de `X`, `Y` y `Z`

Las rotaciones permiten modificar la orientación de la herramienta alrededor de los ejes del sistema de referencia. Este movimiento es importante cuando se requiere ajustar el ángulo de ataque de la herramienta, orientar el marcador o modificar la posición angular del efector final.

- Rotación alrededor de `X`: `[PENDIENTE]`
- Rotación alrededor de `Y`: `[PENDIENTE]`
- Rotación alrededor de `Z`: `[PENDIENTE]`

**`Imagen propuesta:`** Evidencia del manipulador realizando una rotación de la herramienta.

---

## Control de velocidad para movimientos manuales

El control de velocidad es un aspecto fundamental en la operación manual del manipulador, ya que permite realizar movimientos más seguros y precisos. En general, las velocidades bajas se utilizan durante la enseñanza de puntos, aproximaciones a objetos o validación de trayectorias. Las velocidades más altas deben utilizarse únicamente cuando la zona de trabajo está libre de obstáculos y el operador tiene certeza de que el movimiento es seguro.

#### Niveles de velocidad

| Nivel | Descripción | Uso recomendado |
|---|---|---|
| Baja | Movimiento lento y controlado | Enseñanza de puntos, aproximaciones y zonas cercanas a objetos |
| Media | Movimiento moderado | Desplazamientos generales con supervisión |
| Alta | Movimiento rápido | Movimientos en zonas despejadas y previamente verificadas |

**`Nota:`** Los niveles exactos de velocidad deben completarse con base en lo observado en la pantalla del teach pendant durante el laboratorio.

#### Cambio entre niveles de velocidad

El cambio entre niveles de velocidad se realiza desde el teach pendant del manipulador. Este procedimiento permite ajustar la rapidez del movimiento manual antes de desplazar el robot.

**`Procedimiento pendiente:`**

1. `[PENDIENTE]` Identificar la opción o tecla de velocidad en el teach pendant.
2. `[PENDIENTE]` Cambiar el nivel de velocidad.
3. `[PENDIENTE]` Verificar el nivel seleccionado en la pantalla.
4. `[PENDIENTE]` Realizar un movimiento corto para comprobar la velocidad.

#### Identificación de la velocidad en pantalla

El nivel de velocidad establecido se identifica en la interfaz del teach pendant. Esta información permite al operador confirmar si el robot se moverá lentamente o con mayor rapidez antes de ejecutar cualquier desplazamiento.

**`Imagen propuesta:`** Captura o fotografía de la pantalla del teach pendant mostrando el nivel de velocidad seleccionado.

---

## Software RoboDK

**RoboDK** es un software de simulación y programación fuera de línea para robots industriales. Su principal ventaja es que permite trabajar con robots de diferentes marcas dentro de una misma plataforma, lo cual facilita el diseño de estaciones virtuales, la generación de trayectorias y la creación de programas compatibles con distintos controladores.

En este laboratorio, RoboDK se utiliza para modelar la estación de trabajo del Motoman MH6, generar una trayectoria polar, simular el movimiento del robot y preparar la ejecución física del manipulador desde el computador.

#### Aplicaciones principales de RoboDK

RoboDK puede utilizarse en diferentes aplicaciones industriales y académicas, entre las cuales se encuentran:

- Simulación de robots industriales.
- Programación fuera de línea.
- Generación de trayectorias.
- Importación de modelos CAD.
- Verificación de colisiones.
- Análisis de alcance del robot.
- Calibración de herramientas y sistemas de referencia.
- Mecanizado robotizado.
- Impresión 3D.
- Soldadura.
- Corte.
- Dispensado.
- Paletizado.
- Manipulación de piezas.

#### ¿Qué hace RoboDK para mover el manipulador?

RoboDK permite construir una estación virtual en la cual se define el robot, la herramienta, la pieza y el sistema de referencia. A partir de esta información, el software calcula las posiciones necesarias para que el manipulador siga una trayectoria determinada.

Cuando el usuario define una trayectoria, RoboDK genera una secuencia de movimientos que pueden ser simulados dentro del entorno virtual. Posteriormente, mediante un postprocesador, el software puede convertir esa trayectoria en un programa compatible con el controlador del robot.

Para el caso de robots Motoman, el programa generado puede estar asociado al formato utilizado por los controladores Yaskawa Motoman, como los archivos de programa tipo `JBI`.

#### ¿Cómo se comunica RoboDK con el manipulador?

La comunicación entre RoboDK y el manipulador puede realizarse de diferentes formas, dependiendo de la configuración del laboratorio. En términos generales, el proceso consiste en:

1. Crear la estación virtual en RoboDK.
2. Seleccionar el modelo del robot Motoman MH6.
3. Definir la herramienta y el sistema de referencia.
4. Programar la trayectoria.
5. Simular el movimiento.
6. Generar el programa mediante el postprocesador correspondiente.
7. Enviar o cargar el programa en el controlador del robot.
8. Ejecutar la trayectoria en el manipulador físico.

**`Nota:`** Esta sección debe completarse indicando si durante el laboratorio se utilizó comunicación directa por red, carga manual del programa, controlador Motoman o algún driver específico de RoboDK.

---

## Comparación entre RoboDK y RobotStudio

A continuación se presenta una comparación general entre **RoboDK** y **RobotStudio**, considerando su enfoque, compatibilidad y utilidad dentro del laboratorio.

| Característica | RoboDK | RobotStudio |
|---|---|---|
| Fabricante | RoboDK | ABB Robotics |
| Enfoque principal | Simulación y programación fuera de línea para múltiples marcas | Simulación y programación fuera de línea para robots ABB |
| Compatibilidad | Robots de diferentes fabricantes | Principalmente robots ABB |
| Lenguaje o salida | Depende del postprocesador del robot | RAPID |
| Uso en el laboratorio | Programación y simulación del Motoman MH6 | Programación y simulación del ABB IRB140 |
| Ventaja principal | Flexibilidad con múltiples marcas | Alta fidelidad con el ecosistema ABB |
| Limitación principal | Puede requerir ajustes según el controlador | Está orientado principalmente a robots ABB |

#### ¿Qué significa RoboDK para este laboratorio?

Para este laboratorio, **RoboDK** representa una herramienta de conexión entre el diseño virtual y la ejecución física del Motoman MH6. Su importancia radica en que permite diseñar una trayectoria, simularla previamente y generar un programa que pueda ser utilizado por el manipulador real.

Además, al no estar limitado a una sola marca, RoboDK resulta útil en laboratorios donde se trabajan diferentes manipuladores industriales.

#### ¿Qué significa RobotStudio frente a RoboDK?

**RobotStudio** es una herramienta especializada en robots ABB. En el laboratorio anterior fue útil porque se trabajó con el manipulador ABB IRB140, permitiendo simular rutinas y trabajar con instrucciones propias del lenguaje RAPID.

Frente a RoboDK, RobotStudio ofrece mayor fidelidad cuando se trabaja con robots ABB, debido a que emplea el controlador virtual de ABB. Sin embargo, RoboDK resulta más flexible cuando se requiere trabajar con robots de diferentes fabricantes, como en este caso con el Motoman MH6.

---

#### Simulación virtual en RoboDK

La simulación en roboDK es bastante sencilla en comparación con la de Robot Studio. Se debe construir un script en python que contena todos los parametros necesarios para que el robot lleve a cabo las trayectorias y movimientos requeridos. A continuación, se puede evidenciar el código en python completo usado para la simulación:


```python
from robodk.robolink import *
from robodk.robomath import *
import math

# Importamos las librerías necesarias para el texto
from matplotlib.textpath import TextPath
from matplotlib.path import Path

#------------------------------------------------
# 1) Conexión a RoboDK e inicialización
#------------------------------------------------
RDK = Robolink()

# Elegir un robot (si hay varios, aparece un popup)
robot = RDK.ItemUserPick("Selecciona un robot", ITEM_TYPE_ROBOT)
if not robot.Valid():
    raise Exception("No se ha seleccionado un robot válido.")

#Conectar al robot físico
#if not robot.Connect():
#    raise Exception("No se pudo conectar al robot. Verifica que esté en modo remoto y que la configuración sea correcta.")

# Confirmar conexión
#if not robot.ConnectedState():
#    raise Exception("El robot no está conectado correctamente. Revisa la conexión.")

print("Robot conectado correctamente.")
#------------------------------------------------
# 2) Cargar el Frame y herramientas
#------------------------------------------------
frame_name = "Frame_from_Target1"
frame = RDK.Item(frame_name, ITEM_TYPE_FRAME)
if not frame.Valid():
    raise Exception(f'No se encontró el Frame "{frame_name}" en la estación.')

robot.setPoseFrame(frame)
robot.setPoseTool(robot.PoseTool())
robot.setSpeed(300)
robot.setRounding(5)

#------------------------------------------------
# 3) Parámetros de posición
#------------------------------------------------
z_surface = 0
z_safe = 50

# --- POSICIÓN DE LA FIGURA ---
offset_x = 500    
offset_y = 0      
escala = 50 

# --- POSICIÓN DEL TEXTO ---
texto_str = "PABLO"
tamano_letra = 40 

# Generamos el path primero para calcular su tamaño y centrarlo
path_temp = TextPath((0, 0), texto_str, size=tamano_letra)
bbox = path_temp.get_extents()
ancho_texto = bbox.width

# Centramos el texto respecto al offset_x de la figura
offset_texto_x = offset_x - 210 
# Lo ponemos debajo del radio inferior de la figura
offset_texto_y = offset_y - (ancho_texto / 2)

#------------------------------------------------
# 4) Movimiento a casa
#------------------------------------------------
target = RDK.Item("Target_Casa", ITEM_TYPE_TARGET)
robot.MoveJ(target)

#------------------------------------------------
# 5) DIBUJAR FIGURA POLAR
#------------------------------------------------
print("Dibujando figura...")
# Punto de aproximación
robot.MoveJ(transl(offset_x, offset_y, z_surface - z_safe))

num_points = 720
full_turn = 2 * math.pi
x_fin_fig = 0
y_fin_fig = 0

for i in range(num_points + 1):
    theta = full_turn * (i / num_points)
    r = (1 - 2 * math.sin(3 * theta)) * escala
    
    x = (r * math.cos(theta)) + offset_x
    y = (r * math.sin(theta)) + offset_y
    
    if i == 0:
        robot.MoveL(transl(x, y, z_surface))
    else:
        robot.MoveL(transl(x, y, z_surface))
    x_fin_fig, y_fin_fig = x, y

robot.MoveL(transl(x_fin_fig, y_fin_fig, z_surface - z_safe))

#------------------------------------------------
# 6) DIBUJAR NOMBRES (ROTADOS Y EN VARIOS RENGLONES)
#------------------------------------------------
# --- CONFIGURACIÓN DE LOS TEXTOS ---
lineas_de_texto = ["PABLO", "MARCO", "DANIEL"]
tamano_letra = 40 
espacio_entre_lineas = 60 # Distancia en milímetros entre cada renglón

angulo = -90 
rad = math.radians(angulo)

x_curr, y_curr = 0, 0

# Recorremos cada palabra de la lista
for indice, texto_str in enumerate(lineas_de_texto):
    print(f"Dibujando renglón {indice + 1}: {texto_str}...")
    
    # Generamos el path para medir esta palabra específica
    path_temp = TextPath((0, 0), texto_str, size=tamano_letra)
    bbox = path_temp.get_extents()
    ancho_texto = bbox.width
    
    # --- CÁLCULO DE POSICIÓN PARA ESTE RENGLÓN ---
    centro_texto_x = offset_x - 200 - (indice * espacio_entre_lineas) 
    centro_texto_y = offset_y       

    vertices = path_temp.vertices
    codigos = path_temp.codes

    for i in range(len(vertices)):
        # 1. Centramos la palabra localmente
        x_orig = vertices[i][0] - (ancho_texto / 2)
        y_orig = vertices[i][1]
        
        # 2. Aplicamos rotación
        x_rot = (-x_orig * math.cos(rad)) - (y_orig * math.sin(rad))
        y_rot = (-x_orig * math.sin(rad)) + (y_orig * math.cos(rad))

        # 3. Posición final en la mesa
        px = x_rot + centro_texto_x
        py = y_rot + centro_texto_y
        
        tipo = codigos[i]

        if tipo == Path.MOVETO:
            # Subir la herramienta si estábamos dibujando
            if i > 0 or indice > 0: 
                robot.MoveL(transl(x_curr, y_curr, z_surface - z_safe))
            
            # Mover al nuevo punto inicial
            robot.MoveJ(transl(px, py, z_surface - z_safe))
            robot.MoveL(transl(px, py, z_surface))
        else:
            robot.MoveL(transl(px, py, z_surface))
        
        x_curr, y_curr = px, py

# Retorno final al terminar todas las palabras
robot.MoveL(transl(x_curr, y_curr, z_surface - z_safe))
robot.MoveJ(target)

```

#### Implementación física en el Motoman MH6

A continuación, se puede evidenciar el código en python completo usado para conectarse al robot y que realice las trayectorias previamente probadas en la simulación:

```python
from robodk.robolink import *
from robodk.robomath import *
import math

# Importamos las librerías necesarias para el texto
from matplotlib.textpath import TextPath
from matplotlib.path import Path

#------------------------------------------------
# 1) Conexión a RoboDK e inicialización
#------------------------------------------------
RDK = Robolink()

# Elegir un robot (si hay varios, aparece un popup)
robot = RDK.ItemUserPick("Selecciona un robot", ITEM_TYPE_ROBOT)
if not robot.Valid():
    raise Exception("No se ha seleccionado un robot válido.")

# Conectar al robot físico
if not robot.Connect():
    raise Exception("No se pudo conectar al robot. Verifica que esté en modo remoto y que la configuración sea correcta.")

# Confirmar conexión
if not robot.ConnectedState():
    raise Exception("El robot no está conectado correctamente. Revisa la conexión.")

print("Robot conectado correctamente.")
#------------------------------------------------
# 2) Cargar el Frame y herramientas
#------------------------------------------------
frame_name = "Frame_from_Target1"
frame = RDK.Item(frame_name, ITEM_TYPE_FRAME)
if not frame.Valid():
    raise Exception(f'No se encontró el Frame "{frame_name}" en la estación.')

robot.setPoseFrame(frame)
robot.setPoseTool(robot.PoseTool())
robot.setSpeed(300)
robot.setRounding(5)

#------------------------------------------------
# 3) Parámetros de posición
#------------------------------------------------
z_surface = 0
z_safe = 50

# --- POSICIÓN DE LA FIGURA ---
offset_x = 500    
offset_y = 0      
escala = 50 

# --- POSICIÓN DEL TEXTO ---
texto_str = "PABLO"
tamano_letra = 40 

# Generamos el path primero para calcular su tamaño y centrarlo
path_temp = TextPath((0, 0), texto_str, size=tamano_letra)
bbox = path_temp.get_extents()
ancho_texto = bbox.width

# Centramos el texto respecto al offset_x de la figura
offset_texto_x = offset_x - 210 
# Lo ponemos debajo del radio inferior de la figura
offset_texto_y = offset_y - (ancho_texto / 2)

#------------------------------------------------
# 4) Movimiento a casa
#------------------------------------------------
target = RDK.Item("Target_Casa", ITEM_TYPE_TARGET)
robot.MoveJ(target)

#------------------------------------------------
# 5) DIBUJAR FIGURA POLAR
#------------------------------------------------
print("Dibujando figura...")
# Punto de aproximación
robot.MoveJ(transl(offset_x, offset_y, z_surface - z_safe))

num_points = 720
full_turn = 2 * math.pi
x_fin_fig = 0
y_fin_fig = 0

for i in range(num_points + 1):
    theta = full_turn * (i / num_points)
    r = (1 - 2 * math.sin(3 * theta)) * escala
    
    x = (r * math.cos(theta)) + offset_x
    y = (r * math.sin(theta)) + offset_y
    
    if i == 0:
        robot.MoveL(transl(x, y, z_surface))
    else:
        robot.MoveL(transl(x, y, z_surface))
    x_fin_fig, y_fin_fig = x, y

robot.MoveL(transl(x_fin_fig, y_fin_fig, z_surface - z_safe))

#------------------------------------------------
# 6) DIBUJAR NOMBRES (ROTADOS Y EN VARIOS RENGLONES)
#------------------------------------------------
# --- CONFIGURACIÓN DE LOS TEXTOS ---
lineas_de_texto = ["PABLO", "MARCO", "DANIEL"]
tamano_letra = 40 
espacio_entre_lineas = 60 # Distancia en milímetros entre cada renglón

angulo = -90 
rad = math.radians(angulo)

x_curr, y_curr = 0, 0

# Recorremos cada palabra de la lista
for indice, texto_str in enumerate(lineas_de_texto):
    print(f"Dibujando renglón {indice + 1}: {texto_str}...")
    
    # Generamos el path para medir esta palabra específica
    path_temp = TextPath((0, 0), texto_str, size=tamano_letra)
    bbox = path_temp.get_extents()
    ancho_texto = bbox.width
    
    # --- CÁLCULO DE POSICIÓN PARA ESTE RENGLÓN ---
    centro_texto_x = offset_x - 200 - (indice * espacio_entre_lineas) 
    centro_texto_y = offset_y       

    vertices = path_temp.vertices
    codigos = path_temp.codes

    for i in range(len(vertices)):
        # 1. Centramos la palabra localmente
        x_orig = vertices[i][0] - (ancho_texto / 2)
        y_orig = vertices[i][1]
        
        # 2. Aplicamos rotación
        x_rot = (-x_orig * math.cos(rad)) - (y_orig * math.sin(rad))
        y_rot = (-x_orig * math.sin(rad)) + (y_orig * math.cos(rad))

        # 3. Posición final en la mesa
        px = x_rot + centro_texto_x
        py = y_rot + centro_texto_y
        
        tipo = codigos[i]

        if tipo == Path.MOVETO:
            # Subir la herramienta si estábamos dibujando
            if i > 0 or indice > 0: 
                robot.MoveL(transl(x_curr, y_curr, z_surface - z_safe))
            
            # Mover al nuevo punto inicial
            robot.MoveJ(transl(px, py, z_surface - z_safe))
            robot.MoveL(transl(px, py, z_surface))
        else:
            robot.MoveL(transl(px, py, z_surface))
        
        x_curr, y_curr = px, py

# Retorno final al terminar todas las palabras
robot.MoveL(transl(x_curr, y_curr, z_surface - z_safe))
robot.MoveJ(target)

```
Como se puede ver, la principal diferencia es que se descomentan las siguientes líneas, que son las usadas para conectarse al robot y para confirmar la conexión.:

```python
# Conectar al robot físico
if not robot.Connect():
    raise Exception("No se pudo conectar al robot. Verifica que esté en modo remoto y que la configuración sea correcta.")

# Confirmar conexión
if not robot.ConnectedState():
    raise Exception("El robot no está conectado correctamente. Revisa la conexión.")
```

---

## Diagrama de flujo de acciones del robot

A continuación se propone la estructura general del diagrama de flujo correspondiente a la ejecución de la trayectoria polar en el Motoman MH6.

1. Inicio del sistema.
2. Verificación del estado del manipulador.
3. Carga de la estación virtual en RoboDK.
4. Definición del robot Motoman MH6.
5. Definición de la herramienta y sistema de referencia.
6. Generación de puntos de la trayectoria polar.
7. Simulación de la trayectoria en RoboDK.
8. Verificación de colisiones y límites del robot.
9. Generación del programa para el controlador Motoman.
10. Envío o carga del programa en el robot.
11. Ejecución física de la trayectoria.
12. Retorno a posición segura.
13. Finalización del proceso.

**`Imagen propuesta:`** Diagrama de flujo de acciones del robot durante la trayectoria polar.

---

## Plano de planta:

A continuación se debe presentar el plano de planta de la estación de trabajo utilizada durante el laboratorio. Este plano debe mostrar la ubicación de los elementos principales que intervienen en la operación del manipulador Motoman MH6.

Elementos sugeridos para el plano:

- Manipulador Motoman MH6.
- Controlador del robot.
- Computador con RoboDK.
- Mesa o superficie de trabajo.
- Pieza o área donde se realiza la trayectoria polar.
- Zona de seguridad.
- Ubicación del operador.

**`Imagen propuesta:`** Plano de planta de la estación de trabajo del Motoman MH6.

---

## Descripción de las funciones y conceptos utilizados:

Durante el desarrollo del script se emplean las siguientes funciones y conceptos de RoboDK y Python.

- **`Robolink`:** Establece la conexión entre el script y la estación de RoboDK.

- **`ItemUserPick` / `Item`:** Seleccionan elementos de la estación (robot, frame, target) por nombre.

- **`Connect` / `ConnectedState`:** Conectan al robot físico y verifican que la conexión sea exitosa.

- **`setPoseFrame` / `setPoseTool`:** Definen el sistema de referencia y la herramienta activa del robot.

- **`setSpeed` / `setRounding`:** Configuran la velocidad de movimiento y el radio de suavizado entre trayectorias.

- **`MoveJ`:** Movimiento por interpolación de juntas, usado para desplazamientos grandes sin trayectoria cartesiana estricta.

- **`MoveL`:** Movimiento lineal del TCP, usado para trazar cada segmento de la figura y del texto sobre la superficie.

- **`transl(x, y, z)`:** Construye la matriz de transformación homogénea correspondiente a una traslación pura.

- **`TextPath`:** Genera los vértices y códigos vectoriales de una cadena de texto mediante matplotlib, que luego se recorren como trayectoria.

- **`Path.MOVETO`:** Código de control que indica un levantamiento de herramienta entre trazos del texto.

- **Curva polar** `r = (1 - 2·sin(3θ)) · escala`: Ecuación que define la figura dibujada, muestreada en 720 puntos sobre [0, 2π].

- **Rotación 2D:** Se aplica una rotación de −90° a los vértices del texto antes de posicionarlos en la mesa.

---


## Evidencias del laboratorio

#### Evidencia de Home 1

**`Imagen propuesta:`** Fotografía del manipulador Motoman MH6 en la posición Home 1.

#### Evidencia de Home 2

**`Imagen propuesta:`** Fotografía del manipulador Motoman MH6 en la posición Home 2.

#### Evidencia del movimiento manual

**`Imagen propuesta:`** Fotografía del teach pendant durante el movimiento manual por articulaciones o cartesiano.

#### Evidencia de RoboDK

**`Imagen propuesta:`** Captura de pantalla de la estación virtual en RoboDK.

#### Evidencia de la trayectoria polar simulada

**`Imagen propuesta:`** Captura de pantalla de la trayectoria polar simulada en RoboDK.

#### Evidencia de la trayectoria polar física

**`Imagen propuesta:`** Fotografía del Motoman MH6 ejecutando la trayectoria polar en el laboratorio.

---

## Vídeos

#### Vídeo de trayectoria polar en RoboDK y escritura simulado

<div align="center">
  <a href="https://www.youtube.com/watch?v=HAfciXf_1t0">
    <img src="https://www.youtube.com/watch?v=HAfciXf_1t0" alt="Vídeo de simulación de la de trayectoria polar en RoboDK y escritura simulado" width="500"/>
  </a>
</div>


#### Vídeo de trayectoria polar en RoboDK y escritura de nombres dentro del laboratorio

<div align="center">
  <a href="https://www.youtube.com/watch?v=asgsZZ6Cp0k">
    <img src="https://www.youtube.com/watch?v=asgsZZ6Cp0k" alt="Vídeo de simulación de la de trayectoria polar en RoboDK y escritura de nombres dentro del laboratorio" width="500"/>
  </a>
</div>

---

## Conclusiones

El desarrollo de este laboratorio permite comprender las diferencias principales entre el manipulador **Motoman MH6** y el **ABB IRB140**, destacando que ambos son robots industriales de seis ejes con una carga útil de 6 kg, pero con diferencias importantes en alcance, entorno de programación y aplicaciones. El Motoman MH6 presenta un mayor alcance, por lo que puede cubrir una zona de trabajo más amplia, mientras que el ABB IRB140 se caracteriza por ser más compacto y estar integrado al entorno de programación RobotStudio.

El uso de **RoboDK** permite simular y programar trayectorias para robots de diferentes fabricantes, lo cual resulta útil en entornos académicos e industriales donde se trabaja con manipuladores de distintas marcas. En este caso, RoboDK funciona como una herramienta para diseñar, validar y preparar una trayectoria polar antes de su ejecución física en el Motoman MH6.

La trayectoria polar permite aplicar conceptos matemáticos al movimiento de un robot industrial, ya que convierte una ecuación definida mediante radio y ángulo en una serie de puntos cartesianos que el manipulador puede seguir. Esto demuestra la relación entre la programación, la geometría y la operación física de sistemas robóticos.

**`Conclusión pendiente:`** Agregar una conclusión basada en la experiencia real del laboratorio, incluyendo errores encontrados, ajustes realizados, comportamiento del robot y resultado final de la trayectoria polar.

---

## Referencias

ABB Robotics. (2021). *IRB 140: Small, powerful, and fast 6-axes robot*. ABB Robotics.  
https://library.e.abb.com/public/0ab091987347463cb06a3cc653d8ddb8/IRB_140_20211001.pdf

ABB Robotics. (s. f.). *RobotStudio Suite*. ABB Robotics.  
https://www.abb.com/global/en/areas/robotics/products/software/robotstudio-suite

RoboDK. (s. f.). *Simulador de brazos robóticos y programación fuera de línea*. RoboDK.  
https://robodk.com/es/

Yaskawa Motoman. (s. f.). *Motoman MH6 datasheet*. Yaskawa Motoman.  
https://assets.robots.com/robots/Motoman/Handling/MOTOMAN_MH6_Datasheet.pdf
