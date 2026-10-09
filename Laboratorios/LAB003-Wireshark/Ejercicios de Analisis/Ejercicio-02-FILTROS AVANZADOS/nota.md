# Análisis de tráfico mediante filtros de Wireshark

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


- Filtros simples.
- Filtros combinados.
- Operadores `AND`, `OR` y `NOT`.
- Comparaciones de valores.
- Búsquedas mediante `contains`.
- Búsquedas mediante `matches`.
- Uso del operador `in`.
- Uso de `upper` y `lower`.
- Conversión mediante `string`.
- Exclusión de tráfico no relevante.
- Refinamiento progresivo de consultas.

Estas capturas documentan no solamente el resultado final, sino también las herramientas utilizadas para llegar a él.
