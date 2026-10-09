# Análisis de tráfico mediante filtros avanzados de Wireshark

## Objetivo

En esta etapa se trabajó con los filtros de visualización de Wireshark, comenzando por expresiones simples y avanzando hacia filtros más específicos y combinados.

El objetivo principal fue aprender a reducir grandes cantidades de tráfico hasta obtener únicamente los paquetes relevantes para una investigación determinada.


---


# Importancia para un entorno SOC

El conocimiento de filtros de Wireshark resulta especialmente importante en tareas de análisis y respuesta ante incidentes.

Un analista puede recibir una captura de tráfico y necesitar determinar rápidamente:

- Qué equipo inició una comunicación.
- Con qué dirección IP se comunicó.
- Qué puertos fueron utilizados.
- Qué protocolos participaron.
- Qué solicitudes HTTP fueron realizadas.
- Qué consultas DNS se generaron.
- Si existe tráfico fuera de lo esperado.
- Qué paquetes contienen determinada información.
- Qué comunicaciones deben investigarse con mayor profundidad.

Los filtros permiten realizar esta primera etapa de clasificación y reducir el ruido antes de continuar con un análisis más detallado.


# Evidencia

Las capturas incluidas en esta sección muestran los diferentes filtros utilizados durante los ejercicios prácticos.

## Filtrar DNS-consultas-tipo-A
![captura de imagen](Filtrar-DNS-consultas-tipo-A.png) 

## Filtrar-paquetes con TTL-10
![captura de imagen](Filtrar-paquetes-con-TTL-10.png)

## Filtrar-paquetes-que-utilizan-Puerto-TCP-4444
![captura de imagen](Filtrar-paquetes-que-utilizan-Puerto-TCP-4444.png)

## Filtrar-Solicitudes-GET-al puerto-80
![captura de imagen](Filtrar-Solicitudes-GET-al-puerto-80.png)

## Filtro-CONTAINS-paquetes-HTTP-con-servidor-Apache
![captura de imagen](Filtro-CONTAINS-paquetes-HTTP-con-servidor-Apache.png)

## Filtro-IN-paquetes-con-puerto-80,443,8080
![captura de imagen](Filtro-IN-paquetes-con-puerto-80,443,8080.png)

## Filtro-MATCHES-paquetes-donde-el-Host-coincida-con-htm-l-php
![captura de imagen](Filtro-MATCHES-paquetes-donde-el-Host-coincida-con-htm-l-php.png)

## Filtro-STRING-muestra-solo-Frames-impares
![captura de imagen](Filtro-STRING-muestra-solo-Frames-impares.png)

Estas capturas documentan no solamente el resultado final, sino también las herramientas utilizadas para llegar a él.
