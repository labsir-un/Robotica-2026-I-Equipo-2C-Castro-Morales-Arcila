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

Para este segundo laboratorio de robótica industrial se trabaja con el manipulador Motoman MH6, tomando como referencia la experiencia previa con el ABB IRB140 en RobotStudio. La idea es entender no solo sus características técnicas, sino también su forma de operación, sus posiciones iniciales y la manera en que se integra con un software como RoboDK.

El trabajo parte de una comparación entre ambos robots, considerando aspectos como alcance, carga útil, repetibilidad, velocidades articulares, aplicaciones y entorno de programación. Aunque los dos son manipuladores industriales de seis ejes, cada uno responde a necesidades distintas dentro de una celda de trabajo. En el caso del Motoman MH6, el manipulador como tal cuenta con seis ejes, aunque en el laboratorio se dispone de dos ejes adicionales asociados a la estación, lo cual amplía un poco las posibilidades de operación sin cambiar la estructura principal del robot.

Luego se aborda la operación manual del manipulador, incluyendo movimientos por articulaciones, desplazamientos cartesianos, traslaciones y rotaciones respecto a los ejes de referencia. Esta parte es importante porque permite reconocer cómo responde el robot desde el teach pendant y cómo controlar mejor el TCP durante la enseñanza de puntos.

Finalmente, se utiliza RoboDK para crear la estación virtual, simular movimientos y generar una trayectoria polar que después pueda ejecutarse en el manipulador físico. Así, el laboratorio conecta la comparación técnica, la operación manual y la programación de trayectorias en un mismo proceso práctico.

---

## Comparación técnica entre el Motoman MH6 y el ABB IRB140

A continuación se presenta un cuadro comparativo entre el manipulador **Motoman MH6** y el **ABB IRB140**, considerando sus características técnicas principales.

| Característica | Motoman MH6 | ABB IRB140 |
|---|---|---|
| Fabricante | Yaskawa Motoman | ABB Robotics |
| Tipo de robot | Manipulador industrial articulado | Manipulador industrial articulado |
| Número de ejes | 8 ejes | 6 ejes |
| Carga útil máxima | 6 kg | 6 kg |
| Alcance máximo aproximado | 1422 mm | 810 mm |
| Repetibilidad | ±0.08 mm | ±0.03 mm |
| Masa aproximada | 130 kg | 98 kg |
| Montaje | Piso, pared o techo | Piso, pared o invertido |
| Controlador asociado | DX100 / controlador Motoman | IRC5 |
| Software trabajado | RoboDK | RobotStudio |
| Aplicaciones típicas | Manipulación, ensamble, empaque, dispensado, soldadura y atención de máquinas | Manipulación, ensamble, manufactura flexible, soldadura, limpieza, empaque y automatización industrial |

El Motoman MH6 es un robot industrial de seis ejes, con una carga útil de 6 kg y un alcance aproximado de 1422 mm. Esto le da una zona de trabajo bastante amplia para un manipulador de este tipo, lo cual resulta útil en tareas donde el robot necesita cubrir más espacio sin mover su base. Aunque el manipulador como tal tiene seis ejes, en el laboratorio se cuenta con dos ejes adicionales asociados a la estación, detalle que amplía las posibilidades de operación dentro de la práctica, sin que eso cambie la configuración principal del robot.

El ABB IRB140 también es un robot industrial de seis ejes y maneja la misma carga útil nominal de 6 kg, pero su alcance es menor, cerca de 810 mm. Por esa razón, se adapta mejor a estaciones compactas, donde el espacio disponible es más reducido y se busca trabajar con buena precisión en una celda más cerrada.

Con esta comparación se nota que ambos manipuladores tienen capacidades similares en cuanto a carga, pero se diferencian bastante en el área de trabajo que pueden cubrir. El Motoman MH6 ofrece mayor alcance y por eso resulta más conveniente para trayectorias amplias o estaciones con más separación entre elementos. El ABB IRB140, en cambio, se siente más orientado a celdas compactas y además tiene la ventaja de estar muy integrado al ecosistema de ABB mediante RobotStudio, lo que facilita la simulación y programación cuando se trabaja con esa marca.

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

A partir de las características revisadas, ambos robots se pueden entender como manipuladores industriales de seis grados de libertad, aunque su aplicación no es exactamente la misma. Comparten una carga útil nominal similar, pero cambian bastante en alcance, tamaño de celda y entorno de programación.

El Motoman MH6 destaca por su mayor alcance, cercano a 1422 mm, lo que le permite cubrir una zona de trabajo más amplia sin mover la base. Esto lo hace conveniente para trayectorias largas, manipulación de piezas, empaque, dispensado o atención de máquinas. En el laboratorio, además, aunque el manipulador mantiene sus seis ejes principales, la estación cuenta con dos ejes adicionales, lo que amplía un poco las posibilidades de operación.

El ABB IRB140, en cambio, es más compacto, con un alcance aproximado de 810 mm. Por eso funciona mejor en celdas pequeñas o espacios reducidos, y tiene la ventaja de integrarse directamente con RobotStudio, el lenguaje RAPID y el controlador virtual de ABB. En términos prácticos, el Motoman ofrece mayor cobertura espacial, mientras que el ABB resulta más cómodo para estaciones compactas y trabajos dentro del entorno ABB.

---

## Configuraciones iniciales del Motoman MH6

Durante la operación del manipulador **Motoman MH6** se identificaron dos posiciones de referencia principales, conocidas como **Home 1** y **Home 2**. Estas configuraciones permiten llevar el robot a una postura conocida antes de iniciar una rutina, verificar el estado de los ejes o dejar el manipulador en una posición segura cuando no se está ejecutando una trayectoria.

En el teach pendant se observan las posiciones de cada articulación del robot, identificadas como `S`, `L`, `U`, `R`, `B` y `T`. Estos valores corresponden a la posición interna registrada por el controlador para cada eje, por lo que sirven como referencia para comparar si el robot se encuentra correctamente ubicado en la posición de Home seleccionada.

#### Configuración `Home 1`

La configuración **Home 1** corresponde a una posición de referencia general del manipulador. En la pantalla del teach pendant aparece como **WORK HOME POSITION**, mostrando los valores de origen y la posición actual de cada eje. En este caso, la posición actual del robot prácticamente coincide con los valores definidos para esta configuración, con diferencias muy pequeñas en algunos ejes, lo cual indica que el manipulador se encontraba correctamente ubicado en dicha posición.

| Articulación | Posición en Home 1 |
|---|---|
| `S` | `0` |
| `L` | `-115290` |
| `U` | `-111622` |
| `R` | `1` |
| `B` | `42647` |
| `T` | `1393` |

<div align="center">
  <img src="./rwork_home.png" alt="Fotografía del manipulador Motoman MH6 ubicado en la posición WORK HOME POSITION" width="600"/>
</div>

<div align="center">
  <img src="./work_home.png" alt="Fotografía del teach pendant mostrando los valores de la posición WORK HOME POSITION del Motoman MH6" width="600"/>
</div>

#### Configuración `Home 2`

La configuración **Home 2** corresponde a una segunda posición de referencia del manipulador. En la pantalla aparece como **SECOND HOME POS**, donde se muestran los valores especificados, actuales y la diferencia entre ambos. En la imagen se observa que la diferencia es igual a cero en todos los ejes, lo que indica que el robot se encuentra exactamente en la posición definida como segundo Home.

| Articulación | Posición en Home 2 |
|---|---|
| `S` | `0` |
| `L` | `2037` |
| `U` | `2359` |
| `R` | `0` |
| `B` | `-121` |
| `T` | `1392` |

<div align="center">
  <img src="./rsecond_home.png" alt="Fotografía del manipulador Motoman MH6 ubicado en la posición SECOND HOME POS" width="600"/>
</div>

<div align="center">
  <img src="./second_home.png" alt="Fotografía del teach pendant mostrando los valores de la posición SECOND HOME POS del Motoman MH6" width="600"/>
</div>

## Movimiento manual del manipulador Motoman MH6

Durante la práctica, el movimiento manual del **Motoman MH6** se realizó desde el **teach pendant** del controlador DX100. Esta parte es clave porque antes de ejecutar cualquier rutina desde RoboDK o desde un programa cargado en el controlador, primero hay que entender cómo responde el manipulador cuando se mueve directamente desde el mando. En términos prácticos, aquí se aprende a controlar el robot en modo seguro, revisar su postura, ubicar el TCP y validar que no existan interferencias dentro de la celda.

El teach pendant concentra los elementos principales de operación: el selector de modo `TEACH / PLAY / REMOTE`, los botones `START`, `HOLD` y `EMERGENCY STOP`, las teclas de coordenadas, las teclas de velocidad manual, las teclas de movimiento por eje, el botón `SERVO ON READY` y el `Enable Switch`, ubicado en la parte posterior del mando. Este último es importante porque permite habilitar el movimiento del robot mientras se opera manualmente; si no se presiona correctamente, el manipulador no se desplaza aunque se presionen las teclas de eje.

<div align="center">
  <img src="./tech.png" alt="Distribución general del teach pendant del controlador DX100" width="600"/>
</div>

#### Movimiento por articulaciones

En el modo por articulaciones, el robot se mueve eje por eje. Para el Motoman MH6, las articulaciones principales se identifican como `S`, `L`, `U`, `R`, `B` y `T`. Los ejes `S`, `L` y `U` están más relacionados con el posicionamiento general del brazo, mientras que `R`, `B` y `T` corresponden principalmente a la orientación de la muñeca y de la herramienta.

Para mover el manipulador de esta manera, primero se coloca el selector del pendant en modo `TEACH`. Luego se verifica que el grupo de control activo corresponda al robot, en este caso `R1`, ya que el laboratorio también cuenta con ejes adicionales asociados a la estación. Después se selecciona el sistema de coordenadas mediante la tecla `[COORD]` hasta llegar al modo de articulaciones o `Joint`. Con el robot en este modo, las teclas de eje permiten mover cada articulación en sentido positivo o negativo.

En la botonera se observa que las teclas están organizadas de manera que una misma tecla sirve para el modo articular y para el modo cartesiano. Por ejemplo, cuando se trabaja por articulaciones, las teclas controlan `S- / S+`, `L- / L+`, `U- / U+`, `R- / R+`, `B- / B+` y `T- / T+`. Ya en operación, se presiona `[SERVO ON READY]`, se sostiene el `Enable Switch` y se oprime la tecla del eje que se desea mover. Naturalmente, esto se hace con una velocidad baja al principio, porque cualquier cambio brusco puede acercar la herramienta a una zona no deseada.

#### Movimiento cartesiano

En el modo cartesiano, el movimiento ya no se interpreta como giro independiente de cada articulación, sino como desplazamiento del TCP respecto a un sistema de referencia. Esto resulta mucho más cómodo cuando se quiere aproximar la herramienta a una superficie, seguir una dirección específica o corregir la posición del efector final sin pensar directamente en cada junta del robot.

Para cambiar a este modo, se utiliza nuevamente la tecla `[COORD]`. Según el funcionamiento del DX100, cada pulsación cambia el sistema de coordenadas en el orden `Joint`, `Cartesian/Cylindrical`, `Tool` y `User`. El modo activo se revisa en la zona superior de la pantalla, dentro del área de estado del pendant. Una vez seleccionado el modo cartesiano, las mismas teclas de movimiento pasan a controlar traslaciones y rotaciones del TCP.

En este caso, las teclas marcadas como `X- / X+`, `Y- / Y+` y `Z- / Z+` permiten mover la herramienta linealmente sobre los ejes cartesianos. Las teclas asociadas a `R`, `B` y `T` se usan para modificar la orientación de la herramienta, que en la práctica se interpreta como rotación alrededor de los ejes del sistema de referencia seleccionado. Esta diferencia es importante porque en modo articular se modifica la postura del robot, mientras que en modo cartesiano se busca controlar mejor el comportamiento espacial del TCP.

#### Traslaciones en `X`, `Y` y `Z`

Las traslaciones se usan cuando se necesita desplazar la herramienta sin cambiar demasiado su orientación. En el laboratorio esto sirve para acercar el TCP a la zona de trabajo, corregir la altura respecto a la superficie y ubicar el punto inicial de una trayectoria. Para mover en `X`, `Y` o `Z`, se selecciona el modo cartesiano con `[COORD]`, se activa el servo, se mantiene presionado el `Enable Switch` y luego se presiona la tecla correspondiente a la dirección deseada.

El movimiento en `X` desplaza el TCP hacia el sentido positivo o negativo de ese eje, el movimiento en `Y` corrige la posición lateral según el sistema activo, y el movimiento en `Z` normalmente se usa para subir o bajar la herramienta respecto a la superficie de trabajo. Esta última dirección fue especialmente importante para evitar que la herramienta golpeara la mesa o el material antes de iniciar la trayectoria.

#### Rotaciones alrededor de `X`, `Y` y `Z`

Las rotaciones permiten ajustar la orientación del TCP. En una práctica como esta, donde se trabaja con una trayectoria sobre una superficie, no basta con llegar a un punto; también importa cómo llega la herramienta. Una orientación incorrecta puede hacer que el marcador, punta o herramienta de trazado no contacte bien la superficie, o que llegue con un ángulo poco conveniente.

Desde el pendant, estas rotaciones se realizan usando las teclas asociadas a la muñeca del robot cuando se está en un sistema cartesiano, de herramienta o de usuario. En términos operativos, el usuario selecciona el sistema con `[COORD]`, mantiene habilitado el robot con el `Enable Switch` y utiliza las teclas correspondientes para orientar la herramienta alrededor de los ejes definidos. En el laboratorio, esta operación se entiende más como un ajuste fino de orientación que como un desplazamiento grande del manipulador.

---

## Control de velocidad para movimientos manuales

El control de velocidad manual es uno de los puntos más importantes cuando se opera el Motoman desde el teach pendant. En el DX100, la velocidad manual se cambia con las teclas `[FAST]` y `[SLOW]`, ubicadas en la zona central del mando. Según el manual del controlador, al presionar `[FAST]` la velocidad cambia en el orden `INCH`, `SLOW`, `MED` y `FAST`; al presionar `[SLOW]`, el cambio se hace en sentido contrario, es decir, `FAST`, `MED`, `SLOW` e `INCH`.

| Nivel | Identificación en pantalla | Uso dentro de la operación |
|---|---|---|
| `INCH` | `INCH` | Movimiento muy pequeño o por incrementos, útil para ajustes finos. |
| `SLOW` | `SLW` | Movimiento lento, recomendado para enseñar puntos o acercarse a la pieza. |
| `MED` | `MED` | Movimiento intermedio, útil para desplazamientos controlados dentro de la celda. |
| `FAST` | `FST` | Movimiento rápido, recomendable solo cuando la trayectoria está despejada. |

En la práctica, lo más seguro es iniciar en `INCH` o `SLOW`, sobre todo cuando la herramienta está cerca de la mesa, de una pieza o de cualquier elemento de la estación. Luego, si el recorrido está libre y ya se conoce la dirección del movimiento, se puede aumentar a `MED` o `FAST`. El nivel activo se identifica en la parte superior de la pantalla del teach pendant, dentro del área de estado, junto con la información del modo de coordenadas y del grupo de control activo.

También existe la tecla `[HIGH SPEED]`, que permite aumentar la rapidez mientras se mantiene presionada una tecla de eje. Sin embargo, el propio manual indica que esta función no aplica cuando la velocidad manual está en `INCH`, y en operación real conviene usarla con cuidado, porque reduce el margen de reacción del operador.


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

Los videos deben comenzar con la introducción oficial del laboratorio **LabSIR Intro LabSIR**, de acuerdo con los requerimientos de entrega.

#### Vídeo de trayectoria polar en RoboDK y escritura simulada

<div align="center">
  <a href="https://www.youtube.com/watch?v=HAfciXf_1t0">
    <img src="https://img.youtube.com/vi/HAfciXf_1t0/0.jpg" alt="Vídeo de simulación de trayectoria polar en RoboDK y escritura simulada" width="500"/>
  </a>
</div>

#### Vídeo de trayectoria polar en RoboDK y escritura de nombres dentro del laboratorio

<div align="center">
  <a href="https://www.youtube.com/watch?v=asgsZZ6Cp0k">
    <img src="https://img.youtube.com/vi/asgsZZ6Cp0k/0.jpg" alt="Vídeo de trayectoria polar y escritura de nombres en el laboratorio" width="500"/>
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
