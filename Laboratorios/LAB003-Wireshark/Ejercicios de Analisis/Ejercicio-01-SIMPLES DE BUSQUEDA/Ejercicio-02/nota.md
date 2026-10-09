# Ejercicio 02 - Búsqueda de una cadena en los detalles de los paquetes

## Consigna

Buscar la cadena **`r4w`** en los detalles de los paquetes y responder:

**¿Cómo se llama el artista 1?**

---

## Análisis

Para comenzar la investigación utilicé la función **Edit > Find Packet** de Wireshark.

La búsqueda se configuró para localizar la cadena **`r4w`** dentro de los detalles de los paquetes.

Al realizar la búsqueda, Wireshark encuentra una coincidencia y permite acceder directamente al paquete que contiene la cadena buscada.

---

## Paso 1 - Localizar la coincidencia

Una vez encontrada la coincidencia, analicé el paquete para determinar en qué parte de la comunicación se encontraba la cadena `r4w`.

La coincidencia se encuentra dentro de una comunicación HTTP.

---

## Paso 2 - Analizar la comunicación HTTP

Para visualizar el contenido completo de la comunicación utilicé la opción:

**Follow > HTTP Stream**

Esta herramienta permite reconstruir y visualizar el flujo completo de la comunicación HTTP, facilitando la identificación de información que puede encontrarse distribuida dentro de los paquetes.


---

## Paso 3 - Identificar la información solicitada

Al revisar el contenido del flujo HTTP se puede observar la cadena **`r4w`** en el contenido HTML.

Dentro del mismo contenido también se encuentra la información correspondiente al **artista 1**.

---

## Qué se aprendió en el ejercicio


- Búsqueda de cadenas específicas dentro de una captura.
- Utilización de **Edit > Find Packet**.
- Búsqueda mediante los detalles de los paquetes.
- Utilización de **Follow HTTP Stream** para reconstruir una comunicación.
- Inspección del contenido HTML transmitido.
- Localización de información relevante dentro de un flujo de red.
- Relación entre una cadena encontrada y la información contenida en la comunicación.