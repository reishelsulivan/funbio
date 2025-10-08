<div align="center">

# Fundamentos de Biodiseño: Entregable Nº 7

</div>

<div align="justify">

## 1. Modelos y principios de solución
| **Función**              | **Solución 1**              | **Solución 2**              | **Solución 3**             |
|---------------------------|-----------------------------|-----------------------------|-----------------------------|
| **Distribuir presión**    | Espuma viscoelástica        | Gel de silicona             | Air cushion                 |
| **Reducir fricción**      | Tejido de poliamida         | Tejido de poliéster         | Tejido de algodón           |
| **Absorber sudor**        | Material absorbente         | Canales de ventilación      | Malla 3D transpirable       |
| **Monitorizar presión**   | FSR                         | FlexiForce                  | Sensor capacitivo           |
| **Monitorizar temperatura** | Termistor                 | Sensor infrarrojo           | RTD                         |
| **Fácil poner/quitar**    | Cierre magnético            | Cierre de velcro            | Cremallera                  |
| **Lavable**               | Material impermeable        | Funda desmontable           | Material resistente          |



## 2. Espacio de solución



## 3. ¿Fabricar o adquirir?:
- Sensor de presión — Adquirir. Se comprará un sensor de presión presente en el mercado, preferiblemente el FSR
- Microcontrolador — Adquirir. Se comprará un microcontrolador ESP32
- Batería - Adquirir
- Carcasa para electrónica - Fabricar. Se fabricará únicamente una carcasa para el microcontrolador ESP32.
- Material para el liner - Adquirir.  Se adquirirá el material del liner.
- Fabricación del liner — Fabricar. Se fabricará el liner con costura.

## 4. Secuencia de procesos:
Describir la rutina clínica de uso del sistema
- Montaje en el paciente
El fisioterapeuta prepara la piel del bebé 
Se posiciona el liner con sensores dentro del corsé, asegurando que las zonas de presión coincidan con los puntos anatómicos indicados por el médico.
Se conecta el módulo electrónico (SPS) a los conectores del liner.
Se verifica que todo esté bien colocado y conectado con el recurso de monitoreo
- Calibración
Antes de iniciar, se enciende el módulo electrónico y se conecta al recurso de monitoreo.Se realiza una calibración inicial de presión y temperatura, asegurando que las lecturas correspondan al estado de reposo del paciente.
Durante esta fase (≈10–15 segundos), el niño permanece quieto para registrar el nivel base de presión y temperatura.
A continuación, el fisioterapeuta comprueba la reacción de los sensores ejerciendo suaves presiones manuales en los puntos clave del corsé; el sistema debe mostrar los cambios instantáneamente.
Si se detectan lecturas fuera del rango previsto, se ajusta el liner o el corsé hasta alcanzar uniformidad en las áreas sensorizadas.
Se guarda la calibración y se comienza la terapia.
- Sesión de terapia
Durante su uso, el sistema mide con el sensor de presión cada 2 segundos y el de temperatura cada 10 segundos, recolectando información suficiente para analizar la distribución de carga y el confort térmico del paciente.
Los datos se envían de forma inalámbrica al recurso de monitoreo clínico, donde el fisioterapeuta puede observar las lecturas en tiempo real o analizarlas posteriormente.
Si se detecta un aumento de presión o temperatura (por mala colocación o exceso de sudor), el sistema envía una alerta visual en el recurso de monitoreo, indicando la necesidad de reajustar el corsé.
- Desmontaje
Se apaga el sistema, se desconecta del liner y se retira cuidadosamente el corsé del bebé.
Se retira el liner del corsé si se requiere limpieza o cambio.
- Limpieza:
Antes del lavado, se retiran el módulo electrónico (SPS), los sensores removibles, los cuales se limpian por separado con un paño suave humedecido en alcohol isopropílico al 70 % o con toallitas médicas, sin sumergirlos en agua.
Una vez limpio y seco, se vuelve a insertar la electrónica en sus respectivos bolsillos sellados y se verifica su funcionamiento mediante el recurso de monitoreo antes del siguiente uso.
Diagrama de flujo


## 5. Técnicas de producción

**Electrónica:**
- ESP32.- Se utilizará impresión 3D de polímeros biocompatibles como una carcasa para evitar la incomodidad en el bebé .
  - Costos:  	Debido a que se trabaja con impresión 3D  no requiere de moldes por lo que solo 
		emplea el material necesario sin adicionar costos. Los costos de su producción   
		pueden estimarse entre 2 y 5 dólares por unidad dependiendo del material .
  - Durabilidad: Se optimiza su durabilidad y correcto funcionamiento ya que no se  encuentra expuesto ante caídas o derrame de líquidos .
Facilidad de esterilización: Algunos de los polímeros biocompatibles resisten los procesos de esterilización sin que se dañen o degraden ya que materiales como PETG y PEEK soportan temperaturas de hasta 120 °C. Sumado a esto, se reduce la acumulación de microorganismos debido a su superficie lisa .


## 6. Estaciones de trabajo
Gimnasio  de terapia : Esta estación de trabajo consiste en realizar ejercicios personalizados  de rehabilitación y terapéuticos. Tiene como objetivo recuperar o mejorar la funcionalidad , fuerza o movilidad del paciente .
Es importante que la adquisición del liner vaya acompañada de estas terapias para asegurar una correcta movilidad del paciente de forma cómoda y segura sin riesgo de irritar la piel .
Por otro lado ,para estas sesiones, el especialista debe tener a disposición un dispositivo que le permita monitorear y verificar el correcto funcionamiento del accesorio (ej. bluetooth activado) antes de iniciar con la sesión para evitar incomodidad al momento de realizar los ejercicios. Además , evitar usar en simultáneo equipos de electroterapia o magnetoterapia . 

## 7.Automatización
El sistema cuenta con un nivel medio de automatización, ya que proporciona retroalimentación a través de sensores de temperatura, presión y humedad integrados en el acolchado removible, brindando información útil tanto al grupo médico especializado que supervisa los registros como a los padres o cuidadores, mediante una aplicación comprensible. 
Técnicamente, un nivel medio garantiza que el dispositivo se encargue de interpretar  los datos sensoriales y brinde avisos si se detectan cambios en las condiciones internas (como humedad o temperatura elevada) o presión inadecuada. Esto reduce riesgos y mejora la eficacia del tratamiento, sin reemplazar el criterio profesional. 
Desde el punto de vista clínico, esta elección es adecuada porque el paciente es un niño, y se requiere un equilibrio entre asistencia tecnológica y control humano. El sistema busca facilitar el trabajo terapéutico y permitir al personal especializado evaluar la evolución de la escoliosis congénita del paciente, manteniendo la seguridad y comodidad. Además, la aplicación permite generar reportes diarios, cada tres días o semanales, según lo decida el usuario, facilitando el seguimiento del tratamiento y el monitoreo de la evolución del paciente.
Con respecto a los escenarios de seguridad, en caso de que se detecte una condición anormal —como aumento de temperatura o humedad excesiva— la alerta se enviará automáticamente a través de la aplicación. Esto indica que el sistema está cumpliendo su función de detección. Solo si se presentan falsos positivos, se debe reportar al recurso de monitoreo para que se realice una revisión técnica y se garantice el correcto funcionamiento del dispositivo. Los padres o cuidadores no deben manipular la parte electrónica, ya que requiere conocimientos técnicos.
En caso de falla del sistema, los sensores dejarán de emitir datos y el módulo entrará en “modo inactivo”, evitando lecturas erróneas y posibles confusiones. Por ello, no se requiere un botón de parada de emergencia, debido a que el dispositivo no cuenta con componentes motorizados que representen un riesgo activo. La seguridad se respalda mediante la supervisión del personal especializado y el diseño ergonómico y acolchado del corsé, que evita puntos de presión excesiva y mantiene la comodidad del paciente.
