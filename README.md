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
El MVP se basa en una arquitectura IoT híbrida distribuida que integra sensores, microcontroladores y actuadores conectados mediante Zigbee y Wi-Fi, gestionados a través del protocolo MQTT.
</p>

- **Componentes principales:**
  - **Sensores IoT:** Miden humedad del suelo, temperatura ambiente y pH del sustrato.
  - **Microcontroladores:** Reciben datos de los sensores y los envían a la Raspberry Pi mediante Zigbee.
  - **Raspberry Pi (Gateway IoT):** Procesa y reenvía los datos al servidor central usando Wi-Fi y MQTT.
  - **Servidor Central:** Almacena y analiza los datos para la gestión automatizada del riego.
  - **Actuadores (válvulas de riego):** Se activan o desactivan automáticamente según los valores monitoreados.

### Tecnologías de Comunicación

Se ha optado por una combinación de **Zigbee** y **Wi-Fi**, cada uno con un propósito específico:

- **Zigbee:** Comunicación entre sensores y microcontroladores. **Ventajas:**
  - Bajo consumo energético, permitiendo que los sensores funcionen por largos períodos sin necesidad de reemplazo frecuente de baterías.
  - Capacidad de operar en una red de malla, mejorando cobertura y confiabilidad en el vivero, en el que la comunicación entre nodos no dependen de un único punto de acceso.
  - Alta tolerancia a interferencias, al operar en la banda de 2.4 GHz con protocolos de corrección de errores.
    
- **Wi-Fi:** Comunicación entre la Raspberry Pi y el servidor. **Ventajas:**
  - Mayor ancho de banda para el envío eficiente de datos.
  - Integración con el broker MQTT para gestionar la comunicación de los datos provenientes de Zigbee.
  - Facilita el control remoto del sistema sin necesidad de gateways adicionales.

Otras opciones como Bluetooth, LoRa y redes móviles (4G/5G) fueron descartadas por consumo energético, costos asociados y requerimientos de transmisión de datos.
 
### Funcionamiento del MVP

El sistema opera en tiempo real mediante el siguiente flujo:
1. **Medición:** Los sensores detectan humedad, temperatura y pH, mandando los datos al microcontrolador de cada mesa.
2. **Transmisión:** El microcontrolador envían los datos a la Raspberry Pi mediante Zigbee.
3. **Procesamiento:** La Raspberry Pi actúa como gateway, analizando la información recibida y publicándola en el broker MQTT mediante Wi-Fi.
4. **Distribución y acción:** El broker MQTT, a través de temas específicos, envía los datos a los dispositivos suscriptores:
   - **Toma de decisiones:** El servidor evalúa los datos y activa/desactiva el riego según umbrales predefinidos.
   - **Supervisión remota:** Los encargados del vivero pueden monitorear las condiciones desde una interfaz conectada al sistema.
  
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


### 4.2. Pruebas y Validación


---

## 5. Conclusión


---

## 6. Referencias

---

## 7. Anexos
