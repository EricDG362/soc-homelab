# Ejercicio 06 - Análisis de direcciones resueltas

## Consigna

Investigar las direcciones resueltas de la captura y determinar:

**¿Cuál es la dirección IP del host que empieza por `bbc`?**

---

## Análisis

Para comenzar la investigación utilicé la sección **Resolved Addresses** de Wireshark.

Esta función permite consultar las direcciones que Wireshark ha podido asociar con nombres de host durante el análisis de la captura.

La información puede ser útil para relacionar una **dirección IP** con el **nombre de host** correspondiente y facilitar la identificación de los sistemas que aparecen en el tráfico analizado.

---

## Paso 1 - Acceder a Resolved Addresses

Desde el menú superior de Wireshark seleccioné:

**Statistics > Resolved Addresses**

Al acceder a esta sección se muestra una lista con las direcciones resueltas identificadas dentro de la captura.

La información permite observar diferentes tipos de direcciones junto con los nombres asociados.

---

## Paso 2 - Filtrar el nombre del host

Para localizar rápidamente el host indicado en la consigna utilicé el campo de búsqueda o filtrado disponible en la ventana.

Ingresé la cadena:

    bbc


El filtrado permitió encontrar el host cuyo nombre comienza con **`bbc`**.

En el resultado se puede observar tanto el nombre resuelto del host como la dirección IP asociada.

---

## Qué se aprendiódd 

En este ejercicio aprendí y practiqué:

- Acceso a **Statistics > Resolved Addresses**.
- Interpretación de la información de direcciones resueltas.
- Relación entre nombres de host y direcciones IP.
- Búsqueda y filtrado de nombres específicos.
- Identificación de una dirección IP a partir del nombre de un host.