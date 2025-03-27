# Implementación del MVP de IoT en Cisco Packet Tracer

## Información de la actividad
- **Universidad:** Universidad de La Sabana  
- **Facultad:** Facultad de Ingeniería  
- **Materia:** Internet de las Cosas  
- **Profesor:** Juan Manuel Aranda López King  

## Integrantes del Proyecto
| Nombre | Correo Electrónico |
|--------|-------------------|
| Valentina Alejandra López Romero | valentinalopro@unisabana.edu.co |
| Ana Lucía Quintero Vargas | anaquiva@unisabana.edu.co |
| Mariana Valle Moreno | marianavamo@unisabana.edu.co |

## Estructura de la Documentación
- [1. Introducción](#1-introducción)
- [2. Justificación del Proceso Seleccionado](#2-justificación-del-proceso-seleccionado)
- [3. Diseño del MVP y Tecnologías Seleccionadas](#3-diseño-del-mvp-y-tecnologías-seleccionadas)
- [4. Implementación en Cisco Packet Tracer](#4-implementación-en-cisco-packet-tracer)
- [5. Conclusión](#5-conclusión)
- [6. Referencias](#6-referencias)
- [7. Anexos](#7-anexos)

---

## 1. Introducción
<p align="justify">
En el desarrollo de una solución IoT para la empresa Vivero Plantaciones Ravelo, se ha seleccionado como proceso la automatización del riego, específicamente en la zona de cultivo y bandejas de plantas ornamentales. Este proceso es crucial para optimizar el uso del agua, mejorar la eficiencia operativa y garantizar el crecimiento óptimo de las plantas a través del monitoreo y control inteligente. 
  
Para la validación inicial, la conectividad de este MVP (Producto Mínimo Viable) se implementa en Cisco Packet Tracer, permitiendo simular y evaluar su funcionamiento antes de una posible implementación real.
</p>

---

## 2. Justificación del Proceso Seleccionado
<p align="justify">
El riego automatizado en viveros es un desafío que requiere supervisión constante para evitar el desperdicio de agua y garantizar condiciones óptimas para el cultivo. Actualmente, este proceso se realiza manualmente, lo que limita la eficiencia y la precisión en el riego.
</p>

En este conxto, la integración de una solución IoT trae beneficios como:
- **Mayor eficiencia operativa:** Se minimiza la necesidad de intervención humana en el proceso de riego.
- **Reducción del desperdicio de agua:** Se optimiza el consumo mediante riego automatizado basado en datos en tiempo real, activandose solo cuando sea necesario.
- **Supervisión y control remoto:** Permite monitorear el sistema desde cualquier lugar.

La implementación del MVP incluirá sensores para medir **humedad del suelo, temperatura ambiente y pH del sustrato**, datos clave para la automatización del riego.

---

## 3. Diseño del MVP y Tecnologías Seleccionadas

### Arquitectura del sistema
<p align="justify">
El MVP se basa en una arquitectura IoT híbrida distribuida que integra sensores, microcontroladores y actuadores conectados mediante Zigbee y Wi-Fi/Ethernet, gestionados a través del protocolo MQTT.
</p>

- **Componentes principales:**
  - **Sensores IoT:** Miden humedad del suelo, temperatura ambiente y pH del sustrato.
  - **Microcontroladores:** Procesan las mediciones y las envían a la Raspberry Pi vía Zigbee.
  - **Raspberry Pi (Gateway IoT):** Reenvía los datos al servidor central usando Wi-Fi y MQTT.
  - **Servidor Central:** Analiza la información y gestiona la activación del riego.
  - **Actuadores (válvulas de riego):** Se activan o desactivan automáticamente según los valores monitoreados.

### Tecnologías de Comunicación

Se ha optado por una combinación de **Zigbee** y **Wi-Fi/Ethernet**, cada uno con un propósito específico:

- **Zigbee:** Comunicación entre sensores y microcontroladores. **Ventajas:**
  - Bajo consumo energético, permitiendo que los sensores funcionen por largos períodos sin necesidad de reemplazo frecuente de baterías.
  - Capacidad de operar en una red de malla, mejorando cobertura y confiabilidad en el vivero, en el que la comunicación entre nodos no dependen de un único punto de acceso.
  - Alta tolerancia a interferencias, al operar en la banda de 2.4 GHz con protocolos de corrección de errores.
    
- **Wi-Fi/Ethernet:** Comunicación entre la Raspberry Pi y el servidor. **Ventajas:**
  - Mayor ancho de banda para el envío eficiente y estable de datos.
  - Integración con el broker MQTT para gestionar la comunicación de los datos provenientes de Zigbee.
  - Facilita el control remoto del sistema sin necesidad de gateways adicionales.

Otras opciones como Bluetooth, LoRa y redes móviles (4G/5G) fueron descartadas por consumo energético, costos asociados y requerimientos de transmisión de datos.
 
### Funcionamiento del MVP

El sistema opera en tiempo real con el siguiente flujo:

1. **Medición y transmisión:** Los sensores detectan humedad, temperatura y pH, mandando los datos al microcontrolador de cada mesa, el cual los envía a la Raspberry Pi mediante Zigbee.
3. **Procesamiento y comunicación:** La Raspberry Pi actúa como gateway, publicando la información en el broker MQTT mediante Wi-Fi.
4. **Distribución y control:** A través de los temas específicos, se mandan los datos a los dispositivos suscriptores:
   - **Toma de decisiones:** El servidor central analiza los datos y activa/desactiva el riego según umbrales predefinidos.
   - **Supervisión remota:** Los encargados del vivero pueden monitorear las condiciones a través de una interfaz conectada al sistema.
  
Este diseño permite optimizar el consumo de agua y mejorar la eficiencia del riego en el vivero, facilitando su gestión a través de una solución escalable y automatizada.

### Protocolo de Comunicación

El protocolo **MQTT (Message Queuing Telemetry Transport)** se utilizará para la comunicación entre la Raspberry Pi y el servidor debido a las siguientes razones:
- Protocolo ligero, ideal para dispositivos IoT con recursos limitados.
- Opera con un modelo **publish-subscribe**, que permite una comunicación eficiente sin sobrecargar la red.
- Soporte para **QoS (Quality of Service)**, asegurando la entrega confiable de mensajes críticos como la activación del riego.

<p align="justify">
Otras opciones consideradas fueron HTTP y CoAP. Sin embargo, HTTP es demasiado pesado para dispositivos IoT, mientras que CoAP, aunque eficiente, no ofrece la misma flexibilidad y compatibilidad con plataformas ya existentes.
</p>

---

## 4. Implementación en Cisco Packet Tracer

### 4.1. Configuración de la Simulación

Dado que Cisco Packet Tracer no soporta Zigbee ni MQTT, se adaptó la implementación del diseño de la arquitectura IoT, llevándose a cabo los siguientes pasos:
1. **Configuración de la Red Wi-Fi:**
    - Se añadió un ***Home Gateway*** como punto de acceso Wi-Fi para los dispositivos IoT.
    - Se conectó un switch opcional para permitir conexiones cableadas.
    - Se integró un servidor mediante Ethernet para la gestión de datos.
    - Se activó el servicio ***DHCP*** en el Home Gateway para asignación automática de direcciones IP.
2. **Adición de sensores y microcontroladores:**
    - Se colocaron los sensores: ***IoT Soil Moisture, IoT Temperature e IoT Humidity***.
    - Se agregaron IoT Microcontrollers para gestionar la comunicación de los sensores.
    - Se conectaron a la red Wi-Fi a través del Home Gateway.
3. **Configuración de la Raspberry Pi (SBC):**
    - Se añadió un ***Single Board Computer (SBC)*** simulando la Raspberry Pi.
    - Se configuró como cliente HTTP para enviar datos al servidor mediante comandos ***wget***.
4. **Incorporación de Actuadores:**
    - Se incluyeron dispositivos IoT actuadores: aspersores de riego, ventiladores y luces.
    - Se configuraron reglas en el servidor para su activación automática según los datos recibidos.
5. **Configuración del Servidor y Dashboard:**
    - Se activó el servicio ***HTTP Server*** en el servidor.
    - Se creó una página web simulada en index.html para visualizar datos y controlar actuadores.

### 4.2. Pruebas y Validación

Para validar el correcto funcionamiento de la simulación en Cisco Packet Tracer, se realizaron las siguientes pruebas:
- **Verificación de Conectividad:**
    - Se comprobó que los sensores enviaban datos al microcontrolador.
    - Se verificó que la Raspberry Pi recibía datos y los enviaba al servidor mediante HTTP.
    - Se utilizó un navegador web en la Raspberry Pi para acceder a la interfaz del servidor.

- **Pruebas de Control de Actuadores:**
    - Se activaron los actuadores desde la página web del servidor.
    - Se verificó la respuesta de los dispositivos al recibir comandos de activación/desactivación.

- **Desafíos y Soluciones:**
<p align="justify">
Para la simulación en Cisco Packet Tracer, inicialmente se encontró el problema de que no hay soporte para tecnologías como Zigbee ni MQTT. Por tanto, como alternativas se usaron únicamente Wi-Fi y HTTP para la comunicación. 

---

## 5. Conclusión


---

## 6. Referencias

---

## 7. Anexos
