<div align="center">

# Fundamentos de Biodiseño: Entregable Nº 11

</div>
<div align="center">
  
</div>

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

