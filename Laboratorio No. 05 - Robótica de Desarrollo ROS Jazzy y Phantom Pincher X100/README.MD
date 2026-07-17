<div align="center">
  <picture>
    <source srcset="https://imgur.com/5bYAzsb.png" media="(prefers-color-scheme: dark)">
    <source srcset="https://imgur.com/Os03JoE.png" media="(prefers-color-scheme: light)">
    <img src="https://imgur.com/Os03JoE.png" alt="Escudo de la Universidad Nacional de Colombia" width="350px">
  </picture>

  <h1>Laboratorio No. 05 </h1>
  <h2>Phantom X Pincher X100 - ROS 2 Jazzy - RViz</h2>

  <p>
    <strong>Robótica - 2026-I</strong><br>
    Ingeniería Mecatrónica<br>
    Facultad de Ingeniería<br>
    Universidad Nacional de Colombia
  </p>
</div>


## Integrantes

* **Pablo de Jesús Arcila Mora**
* **Marco Alejandro Morales Pantoja**
* **Daniel Felipe Castro Galindo**


### Descripción general del laboratorio

Este repositorio presenta el desarrollo del **Laboratorio No. 05** de Robótica, enfocado en el control, modelado geométrico y análisis cinemático del manipulador **Phantom X Pincher X100** empleando **ROS 2 Jazzy**, **Python 3** y **RViz**.

La solución implementada, que se describirá, se realizo mediante un analisis del manipulador con la finalidad de mediante la resolución de la cinemática directa e invers, desarrollar rutinas y coreografias con el **Phanton X**, todo ello, tomando como base para la manipulacion del mismo, la informacion suministrada en el repositorio [PhantomX Pincher X100 con ROS 2 Jazzy](https://github.com/labsir-un/06_Rob_2026_I_ROS2_Jazzy_PhantomX100_RVIZ)

## Diagrama de flujo de las acciones del robot

## Desarrollo del taller

### Identificación de motores y articulaciones

Se realizó la identificación mediante simulación de cada una de las articulaciones del manipulador: base, hombro, codo, muñeca y pinza, junto con el identificador DYNAMIXEL de cada servomotor, el sentido positivo de movimiento y la posición de referencia asociada. Dicha caracterización fue necesaria para construir correctamente los nodos de control articular y para asociar de manera consistente cada comando con la articulación correspondiente.

| Articulación | ID | Referencia | Sentido positivo | Función |
|---|---:|---|---|---|
| Base | `--` | `--` | `--` | Rotación principal del brazo |
| Hombro | `--` | `--` | `--` | Elevación del primer eslabón |
| Codo | `--` | `--` | `--` | Extensión y repliegue del brazo |
| Muñeca | `--` | `--` | `--` | Orientación final del efector |
| Pinza | `--` | `--` | `--` | Apertura y cierre |

### Medición del robot

La geometría del robot podía obtenerse mediante la medicion de los archivos STL de las piezas que componen el **Phantom X** encontradas en el repositorio [Modelos 3D Phantom X](https://github.com/labsir-un/06_Rob_2026_I_ROS2_Jazzy_PhantomX100_RVIZ). A partir de estas mediciones se determinaron las siguientes dimensiones:

#### Dimensiones geométricas del robot

| Parámetro | Valor | Unidad | Observaciones |
|---|---:|---|---|
| Altura de la base |  | mm | Distancia vertical desde la base hasta el primer eje articular. |
| Distancia entre ejes consecutivos 1–2 |  | mm | Separación entre la base y el hombro. |
| Distancia entre ejes consecutivos 2–3 |  | mm | Separación entre hombro y codo. |
| Distancia entre ejes consecutivos 3–4 |  | mm | Separación entre codo y muñeca. |
| Distancia entre ejes consecutivos 4–TCP |  | mm | Distancia desde la última articulación hasta el TCP. |

#### Longitudes de eslabones

| Eslabón | Valor | Unidad | Observaciones |
|---|---:|---|---|
| Eslabón 1 |  | mm | Primer tramo del brazo. |
| Eslabón 2 |  | mm | Segundo tramo del brazo. |
| Eslabón 3 |  | mm | Tercer tramo del brazo. |
| Eslabón 4 |  | mm | Tramo final antes del efector. |

#### Dimensiones principales de la pinza

| Dimensión | Valor | Unidad | Observaciones |
|---|---:|---|---|
| Ancho total de la pinza |  | mm | Medida exterior máxima. |
| Largo de cada dedo |  | mm | Longitud útil de los dedos de agarre. |
| Separación máxima de apertura |  | mm | Distancia máxima entre mordazas. |
| Espesor de la pinza |  | mm | Grosor estructural del conjunto. |
| Distancia de la pinza al TCP |  | mm | Punto de referencia de la herramienta. |


### Movimiento individual de articulaciones

Para cada articulación se ejecutaron las siguientes posiciones analizando los límites seguros del **Phantom X**, para luego retornarlo a la posición de referencia, con el fin de validar el sentido de movimiento y la respuesta del sistema. Toda esta implementacion llevada a cabo en el simulador. 



### Determinación de límites seguros

Mediante la simulacion en **Rviz** se comprobaron límites seguros para cada articulación tomando en cuenta, hasya que zonas el manipulador real puede llegar a alcanzar los topes mecánicos del robot, esto con el fin de que al momento de construir las rutinas, el manipulador no este fuera de los intervalo permitidos, quedando de la siguiente manera:

| Articulación | Límite inferior | Límite superior | Margen de seguridad |
|---|---:|---:|---:|
| Base | `--` | `--` | `--` |
| Hombro | `--` | `--` | `--` |
| Codo | `--` | `--` | `--` |
| Muñeca | `--` | `--` | `--` |
| Pinza | `--` | `--` | `--` |

### Cinemática directa

En base al **Phantom X** se realizo un analisis con el fin de obtener los parámetros Denavit-Hartenberg del manipulador e implementar la cinemática directa del robot a partir de ellos. Prara ello, en matlab se desarrollo un programa que recibe las variables articulares \(q_1, q_2, q_3, q_4\) y calcula la posición y orientación del efector final en términos de \(x, y, z, roll, pitch, yaw\)

#### Parámetros DH

| Eslabón | \(a_i\) | \(\alpha_i\) | \(d_i\) | \(\theta_i\) |
|---|---:|---:|---:|---:|
| 1 | `--` | `--` | `--` | \(q_1\) |
| 2 | `--` | `--` | `--` | \(q_2\) |
| 3 | `--` | `--` | `--` | \(q_3\) |
| 4 | `--` | `--` | `--` | \(q_4\) |

#### Codigo MATLAB


### Cinemática inversa


### Enseñanza y repetición de poses


### Trazado de una figura


### Coreografía robótica


## Código fuente


## Plano de planta


## Video Explicativos 

### Video del movimiento individual, simultáneo y secuencial

### Video de enseñanza y repetición de poses

### Video del trazado de figuras

### Video completo de la coreografía robótica



## Conclusiones individuales

### **Pablo de Jesús Arcila Mora**

### **Daniel Felipe Castro Galindo**

### **Marco Alejandro Morales Pantoja**


