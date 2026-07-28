<div align="center">
  <picture>
    <source srcset="https://imgur.com/5bYAzsb.png" media="(prefers-color-scheme: dark)">
    <source srcset="https://imgur.com/Os03JoE.png" media="(prefers-color-scheme: light)">
    <img src="https://imgur.com/Os03JoE.png" alt="Escudo de la Universidad Nacional de Colombia" width="350px">
  </picture>

  <h1>Proyecto Final- Robótica Industrial</h1>
  <h2>Automatización del Proceso de Ensamblaje, Soldadura y Empaque de PCBs.</h2>

  <p>
    <strong>Robótica - 2026-I</strong><br>
    Ingeniería Mecatrónica<br>
    Facultad de Ingeniería<br>
    Universidad Nacional de Colombia
  </p>
</div>



## Integrantes

* **Pablo de Jesus Arcila Mora**
* **Marco Alejandro Morales Pantoja**
* **Daniel Felipe Castro Galindo**
* **Juan ... ... ...**
* **Alejandra ... ... ...**

### Bitácora del desarrollo

### Diagrama de flujo del proceso global y por estación (robots) con estados y fallas

```mermaid
flowchart TD
    Inicio([Sistema IDLE]) --> E1_READY[Etapa 1 Caín - READY: verificar estado seguro]
    E1_READY --> E1_RUN[Etapa 1 RUN: recibir componente de banda]
    E1_RUN --> E1_Pick{Pick exitoso?}
    E1_Pick -- No, reintentar N veces --> E1_RUN
    E1_Pick -- Fallo persistente --> E1_FAULT[FAULT: alarma pick fallido]
    E1_FAULT --> E1_RUN
    E1_Pick -- Sí --> E1_Clas{Clasificación cierta?}
    E1_Clas -- No --> E1_Rechazo[Enviar a bandeja Rechazo / confirmar en HMI]
    E1_Rechazo --> E1_RUN
    E1_Clas -- Sí --> E1_Place[Colocar en celda del almacén]
    E1_Place --> E1_Conteo{Almacén con 30+ componentes?}
    E1_Conteo -- No --> E1_RUN
    E1_Conteo -- Sí --> E1_DONE[Etapa 1 DONE: Almacén Listo]

    E1_DONE --> E2_READY[Etapa 2 Junior - READY: PCB fijada en fixture]
    E2_READY --> E2_RUN[Etapa 2 RUN: tomar componente del almacén]
    E2_RUN --> E2_Pick{Componente disponible en celda?}
    E2_Pick -- No, agotado --> E2_FAULT[FAULT: alarma componente agotado, solicitar reposición]
    E2_FAULT --> E2_RUN
    E2_Pick -- Sí --> E2_Insert[Insertar/colocar en PCB]
    E2_Insert --> E2_Check{Place correcto?}
    E2_Check -- No --> E2_Repro[Marcar como Reproceso]
    E2_Repro --> E2_RUN
    E2_Check -- Sí --> E2_Cont{Receta completa 30+?}
    E2_Cont -- No --> E2_RUN
    E2_Cont -- Sí --> E2_DONE[Etapa 2 DONE: PCB Poblada]

    E2_DONE --> E3_READY[Etapa 3 Chambeador - READY: PCB fijada en estación soldadura]
    E3_READY --> E3_Fix{PCB fijada correctamente?}
    E3_Fix -- No --> E3_FAULT1[FAULT: detener y solicitar ajuste]
    E3_FAULT1 --> E3_READY
    E3_Fix -- Sí --> E3_RUN[Etapa 3 RUN: ejecutar rutina de soldadura por puntos]
    E3_RUN --> E3_Emerg{Parada de emergencia activada?}
    E3_Emerg -- Sí --> E3_FAULT2[FAULT: reset y home seguro]
    E3_FAULT2 --> E3_READY
    E3_Emerg -- No --> E3_Verif{Todos los puntos soldados?}
    E3_Verif -- No --> E3_RUN
    E3_Verif -- Sí --> E3_DONE[Etapa 3 DONE: PCB Soldada]

    E3_DONE --> E4_READY[Etapa 4 Abel - READY: recibir PCB soldada]
    E4_READY --> E4_RUN[Etapa 4 RUN: empacar y enviar por banda]
    E4_RUN --> E4_Conf{Confirmación de salida OK?}
    E4_Conf -- No --> E4_FAULT[FAULT: alarma, reintentar empaque]
    E4_FAULT --> E4_RUN
    E4_Conf -- Sí --> E4_DONE[Etapa 4 DONE: PCB empacada y enviada]

    E4_DONE --> Fin([Fin del ciclo - contador de PCBs incrementa])
```

## Diseño del gripper/herramienta de soldadura

Para la Etapa 3 del proyecto se diseñó una herramienta terminal para el robot Yaskawa Motoman MH6, denominado **“El Chambeador”**, cuya función es sostener el cautín y permitir la ejecución controlada de los puntos de soldadura sobre la PCB.

La herramienta se dividió en dos componentes principales: una **base de fijación** y un **cuerpo tubular portacautín**. Esta configuración modular facilita la fabricación mediante impresión 3D, el montaje del cautín y el reemplazo independiente de cualquiera de las piezas.

![Base de fijación de la herramienta](./IMG/BASE.png)

*Figura 1. Base de fijación y sistema de acople de la herramienta.*

La base incorpora los orificios necesarios para su sujeción al sistema de montaje del robot. En su parte frontal se diseñó un alojamiento circular con ranuras que recibe las pestañas del cuerpo portacautín.

![Cuerpo tubular portacautín](./IMG/PUNTA.png)

*Figura 2. Cuerpo tubular encargado de alojar y sujetar el cautín.*

### Sistema de acople

La unión entre las dos piezas funciona mediante un mecanismo de acople por inserción y giro, similar a un cierre de bayoneta. Para ensamblar la herramienta, las pestañas del cuerpo tubular se alinean con las ranuras de la base, se introduce la pieza y posteriormente se realiza un giro hasta alcanzar la posición de bloqueo.

Este sistema permite montar y desmontar rápidamente el cautín sin retirar toda la base del robot. Además, restringe el desplazamiento axial accidental durante la rutina y ayuda a conservar una posición definida de la herramienta con respecto al TCP programado.

### Compensación axial mediante resorte

Entre el cautín y su superficie de apoyo se instaló un resorte que proporciona **compliancia axial pasiva**. Cuando la punta entra en contacto con el punto de soldadura, el cautín puede desplazarse ligeramente en dirección longitudinal en lugar de transmitir toda la fuerza directamente a la PCB.

Esta solución permite:

- Compensar pequeñas variaciones en la altura o planitud de la PCB.
- Absorber errores menores de posicionamiento y calibración del robot.
- Reducir el riesgo de aplicar una fuerza excesiva sobre las pistas, terminales o componentes.
- Evitar impactos rígidos que puedan deteriorar la punta del cautín.
- Mantener un contacto más uniforme durante el tiempo programado de soldadura.

La rigidez y la precarga del resorte deben ajustarse de manera que exista suficiente fuerza para conservar el contacto térmico, sin producir una carga que pueda deformar o dañar la tarjeta.

### Justificación del diseño

El diseño modular y el sistema de compensación axial permiten utilizar un cautín convencional como herramienta terminal para realizar pruebas de soldadura robotizada. La fabricación aditiva hizo posible obtener rápidamente una geometría adaptada tanto al sistema de montaje del robot como al diámetro del cautín, reduciendo el costo y el tiempo de fabricación del prototipo.

La separación en dos piezas también mejora el acceso durante el ensamblaje y facilita las operaciones de mantenimiento. En caso de desgaste, deformación o cambio del cautín, el cuerpo portacautín puede sustituirse sin fabricar nuevamente la base completa.

### Recomendaciones de uso y mejora

Debido a que la herramienta fue fabricada mediante impresión 3D en material polimérico, se recomienda emplearla principalmente en **pruebas controladas y rutinas de soldadura de corta duración**. La zona frontal, al encontrarse más próxima al elemento calefactor, puede acumular calor y sufrir ablandamiento o deformación progresiva.

Para aumentar la seguridad y la vida útil del sistema se recomienda:

- Evitar el contacto directo entre la parte caliente del cautín y las piezas impresas.
- Incorporar un escudo térmico delgado de acero inoxidable, separado del polímero mediante una cámara de aire.
- Añadir una arandela o buje aislante de mica, cerámica u otro material resistente a altas temperaturas.
- Realizar pausas de enfriamiento entre ciclos prolongados.
- Inspeccionar periódicamente el acople, las pestañas y la zona frontal para detectar deformaciones.
- Para una operación repetitiva o continua, sustituir la sección más cercana al calor por un inserto metálico o fabricar esa zona con un material de mayor resistencia térmica.

Estas mejoras permitirían reducir la transferencia de calor por conducción y radiación hacia las piezas impresas, manteniendo la precisión del montaje y disminuyendo el riesgo de que la herramienta pierda su geometría durante la operación.

### Modelos/simulaciones

### Código fuente comentado

### Comparación manual vs automatizado

### Descripción detallada de la solución planteada

### Diagrama de flujo de acciones del robot

```mermaid
flowchart TD
    Start([IDLE: Inicio Estación 3]) --> Conn[Conectar al robot físico / RoboDK]
    Conn --> ConnOK{Conexión establecida?}
    ConnOK -- No --> ErrConn[FAULT: error de conexión, verificar modo remoto/config]
    ErrConn --> Conn
    ConnOK -- Sí --> Home[READY: mover a posición Home]
    Home --> Riel[Desplazarse por riel axial hasta el punto frente a la mesa PCB]
    Riel --> RielOK{Posición en riel confirmada?}
    RielOK -- No --> RielRetry[FAULT: reintentar posicionamiento en riel]
    RielRetry --> Riel
    RielOK -- Sí --> EntA[Esperar señal PCB Poblada desde Etapa 2]
    EntA --> EntB{PCB fijada correctamente en fixture?}
    EntB -- No --> AjusteFixture[FAULT: detener y solicitar ajuste de PCB]
    AjusteFixture --> EntB
    EntB -- Sí --> RUN[RUN: iniciar rutina de soldadura]
    RUN --> Aprox[Mover a punto de aproximación general]
    Aprox --> Pose[Calcular pose base de la PCB - SolveFK]
    Pose --> L1[Calcular pose de aproximación y soldadura del punto i]
    L1 --> L2[Resolver cinemática inversa - SolveIK]
    L2 --> L3[Mover a aproximación del punto]
    L3 --> Emerg{Parada de emergencia activada?}
    Emerg -- Sí --> FaultEmerg[FAULT: detener, reset y home seguro]
    FaultEmerg --> Home
    Emerg -- No --> L4[Descender a punto de soldadura]
    L4 --> L5[Activar herramienta y esperar tiempo de soldadura]
    L5 --> L6[Retornar a punto de aproximación]
    L6 --> L7{Quedan más puntos?}
    L7 -- Sí --> L1
    L7 -- No --> Verif[Verificar log de puntos soldados + evidencia]
    Verif --> VerifOK{Todos los puntos verificados?}
    VerifOK -- No --> Reproceso[FAULT: marcar Reproceso y reintentar]
    Reproceso --> Aprox
    VerifOK -- Sí --> ReturnAprox[Volver al target de aproximación]
    ReturnAprox --> ReturnHome[Volver a Home]
    ReturnHome --> DONE[DONE: entregar señal PCB Soldada a Etapa 4]
    DONE --> Fin([Fin del ciclo de estación])
```

### Plano de planta de la ubicación de cada uno de los elementos

### Descripción de las funciones utilizadas

### Diseño de la herramienta detallado

### Código fuente utilizado para el desarrollo de la práctica

### Vídeo (simulación e implementación con robots reales)
