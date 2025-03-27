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
- [2. Justificación del Proceso Seleccionado](#2-motivación-y-justificación-del-proceso-seleccionado)
- [3. Diseño del MVP y Tecnologías Seleccionadas](#3-diseño-del-mvp-y-tecnologías-seleccionadas)
- [4. Implementación en Cisco Packet Tracer](#4-implementación-en-cisco-packet-tracer)
- [5. Conclusión](#5-conclusión)
- [6. Referencias](#6-referencias)
- [7. Anexos](#7-anexos)

---

## 1. Introducción
<p align="justify">
Actualmente, el Vivero Plantaciones Ravelo, ubicado en Chía, carece de automatización en el riego y cuidado de sus cultivos, lo que reduce su capacidad de respuesta ante cambios en temperatura, humedad y otras condiciones ambientales, lo que puede afectar la eficiencia operativa y el crecimiento óptimo de las plantas.
  
Para abordar esta problemática, se identificó la zona de cultivo en bandejas de plantas ornamentales dentro del invernadero como el área ideal para una solución basada en Internet de las Cosas (IoT). A diferencia de las plantas en bolsas de tierra, estas comparten sustrato, lo que facilita una distribución eficiente de sensores y una mejor gestión del riego.

Como primer paso, se plantea desarrollar un Producto Mínimo Viable (MVP) centrado en la conectividad, asegurando que los sensores de temperatura ambiente, humedad del suelo y pH del sustrato transmitan datos de forma eficiente al sistema de control. El monitoreo automatizado de estas variables permite optimizar el uso del agua, mejorar el rendimiento de los cultivos y reducir el desperdicio de recursos, creando un entorno más eficiente y sostenible [1]. 

Para validar la funcionalidad del sistema, se emplea Cisco Packet Tracer para simular la comunicación entre sensores y sistema antes de una posible implementación real, asegurando que la infraestructura propuesta sea efectiva en la optimización de recursos y la gestión del riego.
</p>

---

## 2. Motivación y Justificación del Proceso Seleccionado
<p align="justify">
El riego automatizado en viveros representa un desafío que exige un monitoreo constante para optimizar el uso del agua y asegurar condiciones óptimas de cultivo. Actualmente, este proceso se realiza manualmente en la empresa, lo que incrementa el riesgo de desperdicio de recursos y limita la eficiencia en la gestión del riego. La adopción de irrigación de precisión permite optimizar el uso del agua, reducir costos y mejorar la calidad del cultivo, beneficiando tanto al productor como al medioambiente [2].
</p>

Para abordar esta problemática, la integración de una solución IoT ofrece ventajas significativas:
- **Mayor eficiencia operativa:** Minimiza la intervención humana en el riego.
- **Uso eficiente del agua:** Reduce desperdicios al activarse solo cuando sea necesario y evita el estrés hídrico en las plantas [2].
- **Monitoreo y control remoto:** Permite supervisar las condiciones del cultivo en tiempo real desde cualquier ubicación.

El MVP incorporará sensores de **humedad del suelo, temperatura ambiente y pH del sustrato**, variables clave para la automatización del riego y la optimización del cultivo.

---

## 3. Diseño del MVP y Tecnologías Seleccionadas

### Arquitectura del sistema
<p align="justify">
El MVP se basa en una arquitectura IoT híbrida y distribuida, integrando sensores, microcontroladores y actuadores conectados mediante Zigbee y Wi-Fi/Ethernet, con gestión a través del protocolo MQTT. Se prioriza una combinación de tecnologías de comunicación para garantizar eficiencia energética, estabilidad de conexión y escalabilidad en el vivero. 
</p>

- **Componentes principales:**
  - **Sensores IoT:** Miden humedad del suelo, temperatura ambiente y pH del sustrato.
  - **Microcontroladores:** Procesan las mediciones y las envían a la Raspberry Pi vía Zigbee.
  - **Raspberry Pi (Gateway IoT):** Coordina la red Zigbee y reenvía los datos al broker MQTT usando Wi-Fi o Ethernet.
  - **Broker MQTT (Servidor de Mensajería):** Recibe y distribuye la información a los sistemas suscriptores.
  - **Servidor Central:** Analiza la información recibida del broker MQTT y gestiona la activación del riego.
  - **Actuadores (válvulas de riego):** Se activan o desactivan automáticamente según los valores monitoreados.

### Tecnologías de Comunicación

Se ha optado por una combinación de **Zigbee** y **Wi-Fi/Ethernet**, cada uno con un propósito específico:

- **Zigbee:** Comunicación entre sensores y microcontroladores. **Razones clave:**
  - Bajo consumo energético, lo que permite que los sensores operen por largos períodos sin reemplazo frecuente de baterías.
  - Topología de red mallada, que permite la comunicación entre dispositivos sin depender de un único punto de acceso, mejorando la cobertura en el vivero y asegurando tolerancia a fallos [4].
  - Alta confiabilidad en la transmisión de datos, al emplear reintentos de paquetes y corrección de errores para garantizar una comunicación precisa, incluso en entornos con interferencias [4].
  - Uso de técnicas de mitigación de interferencias, como el salto de frecuencia en la banda de 2.4 GHz, 868 MHz o 915 MHz, lo que mejora la estabilidad en la comunicación y evita colisiones con otros dispositivos inalámbricos [4].
- Seguridad integrada, con medidas de cifrado y autenticación que protegen los datos transmitidos frente a accesos no autorizados [4].
- Optimizado para aplicaciones de monitoreo, dado que ZigBee opera a bajas velocidades de transmisión, lo que es suficiente para el intercambio eficiente de datos de sensores sin consumir ancho de banda innecesario [4].
    
- **Wi-Fi/Ethernet:** Comunicación entre la Raspberry Pi y el servidor MQTT. **Razones clave:**
  - **Wi-Fi** permite una conexión inalámbrica más flexible, útil en áreas del vivero donde no es factible el cableado.
  - **Ethernet** proporciona una conexión más estable y rápida en zonas donde la señal Wi-Fi pueda ser débil o donde se requiera mayor ancho de banda.
  - La Raspberry Pi no procesa los datos directamente, sino que los reenvía al broker MQTT, usando Wi-Fi o Ethernet según disponibilidad.
  - Ambas tecnologías garantizan una comunicación eficiente con el broker MQTT.

Otras alternativas como Bluetooth Low Energy (BLE), LoRa y redes móviles (4G/5G) fueron descartadas debido a su menor alcance, consumo energético o costos asociados, por más de que algunas son capaces de alcanzar mayores velocidades de transmisión (como en el caso de BLE) [3].

### Protocolo de Comunicación

El protocolo **MQTT (Message Queuing Telemetry Transport)** se utilizará para la comunicación entre la Raspberry Pi, el servidor y los clientes debido a las siguientes razones:
- Protocolo ligero, ideal para dispositivos IoT con recursos limitados, permitiendo una comunicación eficiente
- Opera con un modelo **publish-subscribe**, lo que permite que múltiples dispositivos (sensores, servidores, actuadores) intercambien datos sin conexiones directas.
- Soporte para **QoS (Quality of Service)**, asegurando la entrega confiable de mensajes críticos como la activación del riego.
- Bajo consumo de ancho de banda, ideal para redes con restricciones de conectividad.

<p align="justify">
Otras opciones consideradas fueron HTTP y CoAP. Sin embargo, por un lado HTTP es demasiado pesado para dispositivos IoT, mientras que CoAP, aunque puede llegar a ser eficiente, no ofrece la misma flexibilidad y compatibilidad con plataformas ya existentes.
</p>

### Funcionamiento del MVP

El sistema opera en tiempo real con el siguiente flujo:

1. **Medición y transmisión:** Los sensores detectan humedad, temperatura y pH, mandando los datos al microcontrolador de cada mesa, el cual los envía a la Raspberry Pi mediante Zigbee.
3. **Procesamiento y comunicación:** La Raspberry Pi actúa como gateway, publicando la información en el broker MQTT mediante Wi-Fi o Ethernet.
4. **Distribución y control:** A través de los temas específicos, se mandan los datos a los dispositivos suscriptores:
   - **Toma de decisiones:** El servidor central analiza los datos y activa/desactiva el riego según umbrales predefinidos.
   - **Supervisión remota:** Los encargados del vivero pueden monitorear las condiciones a través de una interfaz conectada al sistema.
  
Este diseño permite optimizar el consumo de agua y mejorar la eficiencia del riego en el vivero, facilitando su gestión a través de una solución escalable y automatizada.

---

## 4. Implementación en Cisco Packet Tracer

### 4.1. Configuración de la Simulación

Para la implementación del diseño de la red IoT en Cisco Packet Tracer, fue necesario adaptar la arquitectura inicial debido a la falta de soporte para tecnologías como Zigbee y MQTT. Como alternativa:
- Se empleó Wi-Fi para la comunicación entre sensores y la Raspberry Pi.
- Se sustituyó MQTT por HTTP como protocolo de transmisión de datos.
- Se configuró un servidor HTTP para almacenar y procesar las lecturas de sensores simuladas.

La selección de los componentes se basó en su compatibilidad con Cisco Packet Tracer y su capacidad de replicar el flujo de información esperado en la red IoT.

A continuación, se presentan los componentes utilizados y su función en la simulación:

| *Componente*              | *Dispositivo en Packet Tracer*          | *Función* |
|-----------------------------|---------------------------------|------------|
| *Sensores IoT*  | *IoT Temperature, IoT Humidity* | Miden condiciones del ambiente y del suelo. |
| *Microcontrolador local (ESP32/Arduino)* | *IoT Microcontroller* | Recibe los datos de los sensores y los transmite a la Raspberry Pi. |
| *Coordinador/Gateway (Raspberry Pi)* | *Single Board Computer (SBC)* | Recibe datos de los microcontroladores y los envía al servidor. |
| *Servidor/Dashboard* | *Server con Web Server activado* | Procesa y muestra los datos del vivero. |
| *Red Wi-Fi* | *Home Gateway (Router Wi-Fi)* | Conecta todos los dispositivos a la red. |
| *Actuadores (Aspersores)* | *IoT Water Sprinkler* | Se activa según condiciones del ambiente. |

Con esta configuración, se logró simular la comunicación entre sensores, microcontroladores y el servidor a través de Wi-Fi y HTTP.

#### Pasos de Implementación:
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
    - Se comprobó que los sensores enviaban datos al microcontrolador usando Wi-Fi.
    - Se verificó que la Raspberry Pi recibía datos y los enviaba al servidor mediante HTTP.
    - Se utilizó un navegador web en la Raspberry Pi para acceder a la interfaz del servidor.

- **Pruebas de Control del Actuador:**
    - Se activó el actuador desde la página web del servidor.
    - Se verificó la respuesta del dispositivo aspersor al recibir comandos de activación/desactivación.

Esta fase aseguró que los principios básicos de la automatización del riego sean funcionales en una implementación real con MQTT y Zigbee.

#### Desafíos y Soluciones:
<p align="justify">
Para la simulación en Cisco Packet Tracer, inicialmente se encontró el problema de que no hay soporte para tecnologías como Zigbee ni MQTT. Por tanto, como alternativas se usaron únicamente Wi-Fi y HTTP para la comunicación. 

---

## 5. Conclusión


---

## 6. Referencias

[1] Tecnología y Proyectos Controla, “Conectividad Agroindustrial,” *Tecnologías Controla*, n.d. [Online]. Disponible en: [https://www.tecnologiascontrola.com.mx/servicios/conectividad-agroindustrial/](https://www.tecnologiascontrola.com.mx/servicios/conectividad-agroindustrial/). [Accedido: 27-mar-2025]. 

[2] Entel Digital, “Gestión de sistema de riego de precisión de aguas y sus beneficios,” *e digital*, 2 de abril de 2024. [Online]. Disponible en: [https://enteldigital.cl/blog/gestion-de-sistema-de-riego-de-precision-de-aguas-y-sus-beneficios](https://enteldigital.cl/blog/gestion-de-sistema-de-riego-de-precision-de-aguas-y-sus-beneficios). [Accedido: 27-mar-2025]. 

[3] Venco, “Qué es ZigBee, cómo funciona y características principales,” *Venco*, 3 de diciembre de 2020. [Online]. Disponible en:  [https://www.vencoel.com/que-es-zigbee-como-funciona-y-caracteristicas-principales/](https://www.vencoel.com/que-es-zigbee-como-funciona-y-caracteristicas-principales/). [Accedido: 27-mar-2025].

[4] Abiertaugr,  “Zigbee,” *Abiertaugr*, n. d. [Online]. Disponible en:  [https://abierta.ugr.es/pluginfile.php/76391/mod_resource/content/2/9_zigbee.html](https://abierta.ugr.es/pluginfile.php/76391/mod_resource/content/2/9_zigbee.html). [Accedido: 27-mar-2025].


---

## 7. Anexos
