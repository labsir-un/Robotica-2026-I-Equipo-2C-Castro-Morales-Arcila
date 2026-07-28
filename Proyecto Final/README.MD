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

### Diseño del gripper/herramientas

### Modelos/simulaciones

### Código fuente comentado

### Comparación manual vs automatizado

### Descripción detallada de la solución planteada

### Diagrama de flujo de acciones del robot

### Plano de planta de la ubicación de cada uno de los elementos

### Descripción de las funciones utilizadas

### Diseño de la herramienta detallado

### Código fuente utilizado para el desarrollo de la práctica

### Vídeo (simulación e implementación con robots reales)
