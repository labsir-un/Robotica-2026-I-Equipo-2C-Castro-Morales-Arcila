# Laboratorio No. 03: Robótica Industrial - Manipulador EPSON T3-401S

## 1. Cuadro Comparativo de Manipuladores
| Característica | EPSON T3-401S | Motoman MH6 | ABB IRB 140 |
| :--- | :--- | :--- | :--- |
| **Carga Máxima** | 3 kg | 6 kg | 6 kg |
| **Alcance** | 400 mm | 1422 mm | 800 mm |
| **Grados de Libertad** | 4 ejes (SCARA) | 6 ejes | 6 ejes |
| **Velocidad Máxima** | J1-J2: 3700 mm/s, J3: 1000 mm/s, J4: 2600°/s | Hasta 1000°/s aprox. según eje | Hasta 200°/s según eje |
| **Aplicaciones Típicas** | Pick & place, ensamblaje de piezas pequeñas, manipulación veloz | Soldadura, empaquetado, cuidado de máquinas, manipulación | Ensamblaje, desbarbado, soldadura, cuidado de máquinas |


## 2. Configuraciones Iniciales (Home)
* **Definición de Home:** [Explicar concepto y procedimiento]
* **Posición articular:** [Detallar grados de cada articulación]

## 3. Operación Manual
* **Modos de Movimiento:**
    * **Articular:** [Procedimiento y teclas]
    * **Cartesiano:** [Procedimiento y teclas para traslación/rotación en X, Y, Z]
* **Control de Velocidad:**
    * **Niveles:** [Listar niveles disponibles]
    * **Cambio de nivel:** [Pasos para realizar el cambio]
    * **Identificación:** [Cómo visualizar el nivel en la pantalla]

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
