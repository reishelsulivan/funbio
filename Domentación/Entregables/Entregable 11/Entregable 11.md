<div align="center">

# Fundamentos de Biodiseño: Entregable Nº 11

</div>
<div align="center">
  
</div>

# Introducción
El presente proyecto consiste en el desarrollo de un liner ortésico con sensores destinado a un menor de dos años con escoliosis congénita, con el objetivo de facilitar el monitoreo del crecimiento de la curvatura y la presión ejercida sobre la columna durante el uso del corsé. El sistema integra componentes electrónicos, mecánicos y digitales, combinando sensores de presión (FSR) y temperatura (DS18B20) conectados a un microcontrolador ESP32 para la adquisición y transmisión de datos en tiempo real. 
# Objetivos
- Diseñar un corsé inteligente integrado con sensores para monitorear la postura y progreso de la escoliosis congénita en niños pequeños.
- Asegurar un montaje y ajuste rápido (menor a 3 minutos) del corsé por parte del cuidador para garantizar la comodidad y seguridad.
- Desarrollar una interfaz comprensible para que el cuidador interprete alertas de sobrepresión, batería y fallos del sensor.

# Verificación del diseño 
## Hardware (Electrónica) 
### Arquitectura: 
ESP32 DevKit V1 (3.3 V, BLE) + FSR a ADC1 + dos T° (DS18B20 cerca del ESP y TMP36 
alejado) + coin vibrador (PWM) + Li-ion 3.7 V + TP4056 + regulador 3.3 V + switch. 
### Pinout y conexiones: 
Usamos dos sensores de temperatura: DS18B20 cerca del ESP32 para vigilar la T° de la 
placa y TMP36 alejado como referencia ambiental. Con esto detectamos de forma robusta 
posibles sobrecalentamientos del módulo (comparando T_near vs T_amb) y activamos 
protección por firmware. La presión se mide con FSR en ADC1 (GPIO32/33/39) con divisor 
10 k y filtro RC por canal para lecturas estables. El motor de vibración se controla por PWM 
(GPIO18) y se alimenta desde 3.3 V o 5 V mediante MT3608 según requiera el módulo. La 
alimentación sigue: batería → TP4056 → switch → regulador 3.3 V (lógica) y MT3608 5 V 
(motor).  
- Control de temperatura:  
	- DS18B20 (Near-ESP): DQ → GPIO19, 4.7 kΩ pull-up a 3.3 V; VDD 3.3 V; GND 
común. 
	- TMP36 (Ambiental/Far-ESP): Vout → GPIO35 (ADC1_CH7); Vcc 3.3 V; GND.  
- FSR 
	- FSR1 → GPIO32, FSR2 → GPIO33, (FSR3 → GPIO39 si lo usas). 
	- Cada canal: FSR a 3.3 V; nodo → MCU con 1 kΩ serie; 10 kΩ a GND (divisor) + 100 
nF a GND cerca del pin. 
- Vibración 
	- IN → GPIO18 (PWM). Alimentación del módulo a 3.3 V o 5 V con MT3608 (solo 
para el motor). Par +/– trenzado y 100 nF junto al módulo. 
Energía:  
	- Batería 3.7 V → TP4056 → SWITCH → Reg 3.3 V → 3V3 (ESP32, FSR, TMP36, 
DS18B20).

### Lógica térmica (por protección): 
- Disparo si T_near ≥ 50 °C o ΔT = |T_near − T_amb| ≥ 10 °C. 
- Acción: limitar PWM del motor, enviar alerta BLE; registrar evento. 
	
### Verificación:  
- T°: provocar ΔT≥10 °C con aire caliente local al ESP; debe disparar protección.  	
- Autonomía: ≥ 8 h (BLE + logging, sin vibración continua). 	
- Vibración: latencia < 200 ms (GPIO18→corriente).

## Manufactura Digital
 El sistema físico se compone de un case principal impreso en 3D, monturas flexibles para los sensores de presión y soportes internos que integran la electrónica liner.
 Estas piezas han sido diseñadas en Onshape bajo criterios de ergonomía, comodidad de uso y facilidad de integración con los módulos electrónicos (ESP32, sensores FSR, DS18B20, TMP36, TP4056, batería Li-ion y módulo de vibración).
El objetivo del diseño digital es proteger la electrónica, mantener su posición estable sobre el cuerpo, permitir el intercambio o mantenimiento de los componentes.
### Diseño y componentes
#### Case principal:
- Contiene el microcontrolador ESP32 y Expansion Board, el módulo TP4056, MT3608, la batería, el switch y el sensor de temperatura DS18B20.
- Incorpora guías para la fijación de los componentes mediante insertos roscados
- Dispone de ranuras para el acceso a conectores (USB, switch, pines de prueba).
- Protege el conjunto.
- Montura de sensores (FSR):
- Sostiene los FSR en posición estable para estar sujeto en el liner.
- Permiten transmitir la presión del cuerpo sin causar incomodidad ni deformar los sensores.
- 
#### Ensamble general
- Fijar ESP32 y módulos al case mediante insertos roscados
- Conectar batería y guiar los cables
- Insertar el conjunto en el bolsillo o zona designada del liner.
- Conectar las monturas de sensores FSR a los cables del case.

#### Verificación
| **Prueba / Criterio** | **Procedimiento (digital)** | **Resultado esperado** | **Estado** |
|------------------------|-----------------------------|------------------------|-------------|
| **Compatibilidad con electrónica** | Revisión en CAD de los espacios para la PCB, batería y conectores. | Todos los componentes encajan sin interferencias ni solapamientos. |  Verificado digitalmente |
| **Ajuste general del ensamblaje** | Ensamble virtual del case, tapa y monturas en Onshape. | Las piezas se ensamblan correctamente, sin colisiones. |  Verificado digitalmente |
| **Montura de sensores** | Verificación de la ubicación y orientación de los alojamientos para los FSR. | Los sensores quedan bien alineados y en las zonas correctas. |  Verificado digitalmente |
| **Tolerancias de encaje** | Revisión de holguras entre partes (0.2–0.4 mm). | El cierre es firme y permite un ensamblaje suave. |  Verificado digitalmente |
| **Accesibilidad de conectores y botones** | Comprobación visual en el modelo 3D. | Los conectores y botones pueden manipularse fácilmente. |  Verificado digitalmente |
| **Peso y volumen estimado** | Cálculo automático en CAD usando densidad del PLA. | Peso total aproximado ≤ 100 g. |  Por comprobar (físico) |
| **Resistencia y durabilidad** | Análisis preliminar del modelo y espesores. | Estructura sin zonas frágiles; resistencia esperada adecuada. |  Por comprobar (prototipo) |
| **Ajuste en uso prolongado** | Simulación de flexión y contacto con el cuerpo. | No debería causar incomodidad o presión excesiva. |  Por comprobar |
| **Mantenimiento y desmontaje** | Evaluación de apertura y cierre en el modelo. | Se puede abrir sin dañar el encaje ni la tapa. |  Por comprobar |

El diseño digital del case y monturas del liner inteligente ha sido verificado digitalmente y cumple con los requerimientos de diseño, compatibilidad electrónica y ergonomía previstos.
 Se encuentra en fase de validación física tras el envío a impresión 3D.

### Tabla de verificación del prototipo

| **Funcionalidad** | **Cumplimiento** |
|--------------------|------------------|
| Mide las fuerzas aplicadas en tiempo real. |  Sí |
| La interacción de los componentes se acciona mediante los sensores de presión. |  Sí |
| Compara las lecturas de ambos sensores de temperatura para detectar sobrecalentamiento. | Sí |
| Presenta un ahorro de energía para más duración de la batería. |  No |
| Presenta un ajuste de fuerzas automáticas. |  No |
| El dispositivo señala si la temperatura del mismo sobrepasa el rango debido. |  Sí |
| Se ajusta si la presión sensada es menor al rango. |  No |
| Se desajusta si la presión sensada es mayor al rango. |  No |
| El dispositivo emite la información a un sistema de monitoreo. |  Sí |
| La aplicación permite obtener, procesar, transmitir y almacenar datos. |  Sí |
