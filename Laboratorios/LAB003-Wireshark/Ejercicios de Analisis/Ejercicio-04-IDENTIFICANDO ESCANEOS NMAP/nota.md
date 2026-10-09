# Identificación de escaneos Nmap mediante Wireshark

## Objetivo

En esta etapa se trabajó con el análisis de tráfico TCP, UDP e ICMP mediante Wireshark para identificar patrones compatibles con escaneos de puertos realizados con Nmap.

El objetivo principal fue aprender a reconocer solicitudes de conexión, respuestas de los equipos analizados y mensajes de error que permiten determinar si un puerto se encuentra cerrado.

A través de filtros de visualización, se investigaron comunicaciones dirigidas a diferentes puertos de una misma dirección IP, prestando atención a las marcas de tiempo, las banderas TCP y los mensajes ICMP generados como respuesta a los paquetes enviados.

---

# Análisis realizado

Se analizó una captura de tráfico de red mediante filtros de visualización de Wireshark, examinando los paquetes TCP, UDP e ICMP asociados a solicitudes dirigidas a diferentes puertos.

Durante el ejercicio se identificaron tres patrones principales:

* Solicitudes TCP SYN seguidas de respuestas RST, ACK.
* Paquetes UDP que provocan respuestas ICMP indicando que el puerto de destino es inalcanzable.
* Mensajes ICMP de tipo 3 y código 3, asociados a puertos UDP cerrados.


## 1. Identificación de un posible escaneo SYN de puertos TCP

**Filtro utilizado:**

```wireshark 
tcp.flags.syn == 1 and tcp.flags.ack == 0
```

Este filtro permite visualizar paquetes TCP que tienen activa la bandera SYN y no tienen activa la bandera ACK.

Estos paquetes suelen utilizarse para iniciar conexiones TCP y también forman parte del comportamiento característico de un escaneo SYN realizado con Nmap.

En la captura se observa una misma dirección IP realizando solicitudes a diferentes puertos en intervalos cortos de tiempo. En la columna `Info` aparecen solicitudes SYN seguidas de respuestas RST, ACK.

La respuesta RST, ACK es compatible con un puerto TCP cerrado o con una conexión rechazada por el equipo de destino.

Este patrón puede indicar una actividad de reconocimiento de puertos, especialmente cuando una misma dirección IP realiza múltiples solicitudes a distintos puertos en un período reducido.

El filtro utilizado identifica los paquetes SYN iniciales, pero no demuestra por sí solo que se trate de un escaneo sigiloso. Para investigar las respuestas se puede utilizar el siguiente filtro adicional:

```wireshark 
tcp.flags.reset == 1 and tcp.flags.ack == 1
```

**Captura 1:**

## 2. Identificación de escaneo de puertos UDP

**Filtro utilizado:**

```wireshark 
udp
```

Este filtro permite visualizar los paquetes que utilizan el protocolo UDP.

En la captura se observan múltiples paquetes asociados a una misma dirección IP y dirigidos a diferentes puertos, registrados en distintos momentos.

Al inspeccionar los paquetes ICMP relacionados con estas comunicaciones, se identificaron respuestas con tipo 3 y código 3, que indican que el puerto de destino es inalcanzable debido a que se encuentra cerrado.

Este comportamiento es compatible con una actividad de reconocimiento de puertos UDP, ya que los paquetes enviados a puertos cerrados pueden provocar respuestas ICMP que permiten inferir el estado del servicio investigado.

El filtro `udp` muestra los paquetes UDP, pero no confirma por sí solo que se esté realizando un escaneo. La conclusión se obtiene al correlacionar las solicitudes a diferentes puertos con las respuestas recibidas.

**Captura 2:**

## 3. Identificación de puertos UDP cerrados mediante ICMP

**Filtro utilizado:**

```wireshark
icmp.type == 3 and icmp.code == 3
```

Este filtro permite visualizar mensajes ICMP de tipo 3 y código 3.

* **ICMP Type 3:** Destination Unreachable (destino inalcanzable).
* **ICMP Code 3:** Port Unreachable (puerto inalcanzable).

Estos mensajes indican que el equipo de destino informa que no puede entregar el datagrama UDP al puerto correspondiente, habitualmente porque no existe un servicio escuchando en ese puerto.

En la captura se observan mensajes `Port Unreachable` que permiten identificar solicitudes UDP dirigidas a puertos cerrados. Los detalles de los paquetes ICMP pueden incluir información sobre el datagrama original, lo que ayuda a determinar qué comunicación provocó la respuesta.

La correlación entre los mensajes ICMP, las direcciones IP y los puertos investigados permite reconstruir parte de la actividad de reconocimiento.

**Captura 3:** 


# Aprendizajes

* Identificación de solicitudes TCP SYN mediante filtros de visualización.
* Interpretación de respuestas TCP RST, ACK.
* Reconocimiento de patrones compatibles con escaneos SYN.
* Identificación de tráfico UDP dirigido a diferentes puertos.
* Interpretación de mensajes ICMP de tipo 3 y código 3.
* Identificación de puertos UDP cerrados mediante mensajes `Port Unreachable`.
* Correlación de direcciones IP, puertos, protocolos y marcas de tiempo.
* Uso de filtros de Wireshark para reducir el tráfico y facilitar la investigación.
* Diferenciación entre una observación técnica y una conclusión sobre la actividad detectada.

# Evidencias adjuntas

* Captura 1: solicitudes TCP SYN a diferentes puertos y respuestas RST, ACK.
* Captura 2: tráfico UDP dirigido a diferentes puertos y respuestas asociadas.
* Captura 3: mensajes ICMP de tipo 3 y código 3 que indican puertos UDP cerrados.
