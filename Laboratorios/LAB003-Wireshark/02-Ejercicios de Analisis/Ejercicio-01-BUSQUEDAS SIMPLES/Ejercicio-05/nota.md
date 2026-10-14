# Ejercicio 05 - Análisis de un flujo HTTP

## Consigna

Ir al **paquete 33790** y seguir el flujo HTTP para visualizar la comunicación con el servidor.

**Pregunta:** ¿Cuál es el número total de artistas?

---

## Paso 1 - Localizar el paquete 33790

Utilicé la opción **Go to Packet** e ingresé el número:

    33790

Wireshark me llevó directamente al paquete correspondiente.


Una vez localizado el paquete, observé que la comunicación correspondía al protocolo **HTTP (Hypertext Transfer Protocol)**.

---

## Paso 2 - Seguir el flujo HTTP

Para visualizar la comunicación completa con el servidor, hice clic derecho sobre el paquete y seleccioné:

**Follow > HTTP Stream**

Esta función permite reconstruir y visualizar el flujo completo de la comunicación HTTP entre el cliente y el servidor.

Al seleccionar esta opción se abre una nueva ventana donde se puede observar el contenido de la comunicación HTTP de forma más completa.

---

## Paso 3 - Buscar información dentro del flujo

La ventana del flujo HTTP permite realizar búsquedas dentro del contenido de la comunicación mediante el campo de búsqueda y el botón **Find**.

Como la consigna solicita determinar el número total de artistas, utilicé como término de búsqueda la palabra:

    artist

La búsqueda permitió localizar dentro de la comunicación una sección donde aparecen enumerados los artistas.

---

## Resultado

Luego de analizar el flujo HTTP correspondiente al paquete **33790** y revisar el contenido de la comunicación con el servidor, se identificaron:

**Total de artistas: 3**

---

## Qué se aprendió 

En este ejercicio aprendí y practiqué:

- Localización de paquetes mediante **Go to Packet**.
- Identificación de tráfico HTTP.
- Seguimiento de una comunicación mediante **Follow > HTTP Stream**.
- Reconstrucción y visualización del contenido de una comunicación HTTP.