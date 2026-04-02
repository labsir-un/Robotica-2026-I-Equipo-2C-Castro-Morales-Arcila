<div align="center">
<picture>
    <source srcset="https://imgur.com/5bYAzsb.png" media="(prefers-color-scheme: dark)">
    <source srcset="https://imgur.com/Os03JoE.png" media="(prefers-color-scheme: light)">
    <img src="https://imgur.com/Os03JoE.png" alt="Escudo UNAL" width="350px">
</picture>

<h2>Laboratorio No. 01 Robótica Industrial- Trayectorias, Entradas y Salidas Digitales.</h2>
</div>

<h3>Solución planteada:</h3>

Para la solución física dentro del laboratorio primero se realizaron mediciones de todo el espacio disponible, es decir, medidas importantes como lo son la distancia del extremo de la banda a la base del manipulador, las dimensiones de la banda y las dimensiones de la caja que teníamos disponible para usar. Seguido a esto procedimos a construir simulaciones que nos permitieran tener cierto grado de certeza del comportamiento real de nuestra rutina antes de instalarla en el robot.

<br><br>

Una vez superada la fase de simulaciones, se procedió a la implementación dentro del laboratorio, lo que nos permitió corregir errores que no contemplamos dentro de las simulaciones y ajustar parámetros, y una vez todo arreglado, se concluyó en una rutina que satisface los requerimientos planteados, la misma se desglosa así:

<br><br>

Para instalar y desinstalar la herramienta se programó una posición de mantenimiento, a la que se puede acceder haciendo uso del botón marcado como "DI_02". Una vez oprimido, se enciende el indicador asociado al mismo y el robot comienza a ejecutar la trayectoria de mantenimiento, cuyo objetivo es posicionar el manipulador de manera que sea sencillo el acceso a la herramienta.

<br><br>

Con el fin de tener certeza de que el desplazamiento de la caja por la banda permitiría dibujar sobre la misma sin tener que hacer mediciones adicionales a las ya realizadas, ya sean de tiempo o distancia, se implementó una rutina de preparación para la rutina principal, a la que se puede acceder haciendo uso del botón marcado como "DI_03". Una vez oprimido, se enciende el indicador asociado al mismo y el robot comienza a ejecutar las trayectorias de preparación, que se encargan de posicionar la herramienta en un punto asociado a una esquina de la caja y detiene el robot durante 30 segundos para que el operario ubique debidamente la misma, una vez superado este tiempo el robot procede a tocar con la punta de la herramienta las esquinas extremas de la caja y detiene el robot durante 5 segundos antes de enviar al manipulador a la posición de home, una vez alcanzada esta posición se enciende la banda durante 7 segundos, esto se hace con el fin de tener una referencia temporal casi exacta del tiempo que debe estar encendida la banda en la dirección opuesta para que la caja coincida con la posición establecida por el operador.

<br><br>

Finalmente, se cuenta con la rutina principal, a la que se puede acceder haciendo uso del botón marcado como "DI_01". Una vez oprimido, se enciende el indicador asociado al mismo y se enciende la banda en la dirección contraria a la ejecutada en la rutina explicada anteriormente. La banda se enciende durante los mismos 7 segundos y se procede a ejecutar las trayectorias de aproximación a la caja y de dibujo, durante esta rutina ningún operario introduce sus manos dentro del área de trabajo del robot. Una vez terminadas las trayectorias de dibujado el robot se envía a la posición de home, espera 5 segundos y enciende la banda durante 2, terminando así la rutina.

<br><br>

---
<h3>Diagrama de flujo de acciones del robot:</h3>
---
<h3>Plano de planta:</h3>
---
<h3>Descripción de las funciones utilizadas:</h3>
---
<h3>Diseño de la herramienta:</h3>
---
<h3>Código en RAPID:</h3>
---
<h3>Vídeos:</h3>
