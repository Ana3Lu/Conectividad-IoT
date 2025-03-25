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
En el marco del desarrollo de una solución basada en IoT, se ha seleccionado un proceso específico dentro de un vivero: la automatización del riego en la zona de cultivo y bandejas de plantas. Este proceso es crucial para optimizar el uso del agua, mejorar la eficiencia operativa y garantizar el crecimiento óptimo de las plantas a través del monitoreo y control inteligente. La implementación de este MVP (Producto Mínimo Viable) se llevará a cabo en Cisco Packet Tracer, permitiendo simular y evaluar su funcionamiento antes de una posible implementación en un entorno real.
</p>

---

## 2. Justificación del Proceso Seleccionado
<p align="justify">
El riego automatizado en viveros es un desafío que requiere supervisión constante para evitar el desperdicio de agua y asegurar que las plantas reciban la cantidad exacta de humedad según sus necesidades. Tradicionalmente, este proceso se realiza de manera manual o con temporizadores fijos que no consideran factores ambientales en tiempo real. Mediante una solución basada en IoT, podemos integrar sensores que midan parámetros como humedad del suelo, temperatura ambiente y pH del sustrato. Con estos datos, el sistema puede tomar decisiones automáticas en tiempo real, activando o desactivando el riego según sea necesario.
</p>

Asimismo, la implementación de una arquitectura IoT en este contexto tiene beneficios como:
- Reducción del desperdicio de agua, optimizando el consumo mediante riego automatizado basado en datos en tiempo real.
- Mayor eficiencia operativa, ya que se minimiza la necesidad de intervención humana en el proceso de riego.
- Supervisión y control remoto, permitiendo a los encargados del vivero monitorear las condiciones del cultivo desde cualquier lugar.

---

## 3. Diseño del MVP y Tecnologías Seleccionadas
<p align="justify">
Para la implementación del MVP, se requiere un diseño que incluya sensores IoT, una red de comunicación eficiente y un sistema de control automatizado. La selección de tecnologías debe garantizar un balance entre simplicidad, eficiencia energética y confiabilidad.
</p>

### 3.1. Red y Protocolos de Comunicación

El MVP utilizará una arquitectura de red híbrida, combinando Wi-Fi para la comunicación de los sensores IoT y Ethernet para el servidor central. La elección de estos medios de comunicación responde a las siguientes razones:
- Wi-Fi permite la conexión inalámbrica de sensores y actuadores, reduciendo la necesidad de cableado y facilitando su instalación en el vivero.
- Ethernet garantiza una conexión estable y de baja latencia para el servidor, asegurando la correcta recepción y procesamiento de datos en tiempo real.

En cuanto a protocolos de comunicación, se ha optado por MQTT (Message Queuing Telemetry Transport) debido a sus ventajas en entornos IoT:
- Es un protocolo ligero, ideal para dispositivos con capacidades limitadas.
- Utiliza un modelo publish-subscribe, permitiendo que múltiples sensores envíen datos sin congestionar la red.
- Su flexibilidad en niveles de QoS (Quality of Service) permite asegurar la entrega de mensajes críticos, como la activación del riego.

<p align="justify">
Otras opciones consideradas fueron HTTP y CoAP. Sin embargo, HTTP es demasiado pesado para dispositivos IoT, mientras que CoAP, aunque eficiente, no ofrece la misma flexibilidad y compatibilidad con plataformas ya existentes.
</p>

### 3.2. Componentes del MVP


### 3.3. Funcionamiento del MVP

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
