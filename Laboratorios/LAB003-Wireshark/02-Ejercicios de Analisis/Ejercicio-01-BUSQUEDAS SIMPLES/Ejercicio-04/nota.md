# Ejercicio 04 - Análisis de Expert Information

## Consigna

Ingresar a la sección **Expert Information** de Wireshark y determinar:

**¿Cuál es el número de advertencias?**

---

## Análisis

Para comenzar el análisis accedí a la sección:

**Analyze > Expert Information**

Esta herramienta permite obtener una visión general de diferentes eventos detectados por Wireshark durante el análisis de una captura.

La sección **Expert Information** agrupa información relevante sobre los paquetes y las comunicaciones, mostrando situaciones que pueden indicar errores, comportamientos inusuales, problemas de comunicación o condiciones que requieren una revisión más detallada.

Es importante aclarar que una alerta mostrada en esta sección **no significa necesariamente que exista actividad maliciosa**. Wireshark utiliza estos indicadores para señalar diferentes condiciones detectadas durante el análisis del tráfico, por lo que posteriormente es necesario revisar los paquetes correspondientes para determinar su significado.

---

## Paso 1 - Acceder a Expert Information

Desde la barra de herramientas de Wireshark seleccioné:

**Analyze > Expert Information**


Al acceder a esta sección se presenta un resumen de los eventos identificados en la captura.

Los eventos se encuentran agrupados visualmente mediante diferentes niveles de severidad, representados por colores.

---

## Paso 2 - Interpretar los indicadores

La ventana de **Expert Information** utiliza diferentes colores para clasificar los eventos encontrados:

- **Verde - Chat:** información relacionada con eventos o comunicaciones consideradas normales o de interés informativo.
- **Celeste - Note:** información que puede ser relevante para el análisis, pero que no representa necesariamente un problema.
- **Amarillo - Warn:** advertencias o condiciones que pueden requerir atención durante el análisis.
- **Rojo - Error:** errores o condiciones que indican algún problema detectado en la comunicación o en el tráfico analizado.

Estas categorías permiten obtener rápidamente una visión general de lo que está ocurriendo dentro de la captura.
