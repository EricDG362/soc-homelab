# Ejercicio 01 - Análisis de paquete y obtención de MD5

## Consigna

Encontrar el **paquete número 12** y leer los comentarios asociados al paquete.

**Pregunta:** ¿Cuál es la respuesta?

---

## Paso 1 - Análisis

El primer paso consiste en localizar el **paquete 12** dentro de la captura utilizando la función `Go to Packet` de Wireshark.

Una vez ubicado el paquete, se revisa la información disponible y, específicamente, los comentarios asociados al paquete.

En lugar de contener directamente la respuesta o una flag, el paquete 12 incluye un comentario que funciona como una pista para continuar la investigación.

El comentario indica que se debe:

1. Dirigirse al **paquete 39765**.
2. Localizar la imagen contenida en dicho paquete.
3. Exportar la imagen como un objeto desde Wireshark.
4. Obtener el valor **MD5** de la imagen mediante la terminal.
5. Utilizar el MD5 obtenido como respuesta final del ejercicio.

---


## Paso 2 - Localizar el paquete 39765

Siguiendo la pista encontrada en el paquete 12, utilicé nuevamente **Go to Packet** para acceder al paquete **39765**.


Al analizar este paquete se puede identificar que contiene una imagen que debe ser extraída de la captura.

---

## Paso 3 - Exportar la imagen

Para obtener la imagen contenida en el tráfico capturado, utilicé la opción de Wireshark para **exportar el objeto** correspondiente.

La imagen fue guardada localmente para poder realizar posteriormente el cálculo de su hash.


---

## Paso 4 - Obtener el hash MD5

Una vez exportada la imagen, utilicé la terminal para calcular su valor **MD5**.

El cálculo se realizó mediante el siguiente comando:

```bash
md5sum imagen