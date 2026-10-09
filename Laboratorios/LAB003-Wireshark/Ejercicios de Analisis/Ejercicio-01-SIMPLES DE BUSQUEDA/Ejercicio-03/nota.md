# Ejercicio 03 - Extracción y análisis de un archivo TXT

## Consigna

Hay un archivo `.txt` dentro de un paquete.

**Pregunta:** ¿Cómo se llama el alienígena?

---

## Análisis

Para comenzar la investigación utilicé nuevamente la función **Edit > Find Packet** de Wireshark.

En esta ocasión realicé una búsqueda utilizando la cadena:

    .txt

La búsqueda permitió localizar una coincidencia relacionada con un archivo llamado **`note.txt`**.

---

## Paso 1 - Identificar el nombre del archivo

La búsqueda llevó al **paquete 1652**, donde se puede observar la coincidencia de `note.txt` dentro del contenido HTML de la comunicación.

En este punto se obtiene una pista importante: conocemos el nombre del archivo que estamos buscando.

Sin embargo, este paquete no contiene necesariamente el archivo. La presencia de `note.txt` dentro del HTML solamente indica o referencia que dicho archivo existe.

Por lo tanto, es necesario continuar la investigación para localizar el archivo realmente transmitido.

---

## Paso 2 - Buscar el archivo entre los objetos HTTP

Con el nombre del archivo identificado, utilicé la opción:

**File > Export Objects > HTTP**

Esta función permite visualizar los diferentes objetos que fueron transferidos mediante HTTP durante la captura.

La ventana muestra los diferentes archivos y objetos HTTP encontrados en los paquetes de la captura.

Para localizar rápidamente el archivo buscado utilicé el campo de filtrado disponible en la ventana e ingresé:

    note.txt

---

## Paso 3 - Localizar el archivo

El filtrado permitió identificar el **paquete 4267**, que contiene el archivo `note.txt`.

Esto permite diferenciar entre:

- **Paquete 1652:** contiene una referencia al archivo `note.txt` dentro del HTML.
- **Paquete 4267:** contiene el archivo `note.txt` que puede ser exportado.

---

## Paso 4 - Exportar y leer el archivo

Una vez identificado el objeto correcto, exporté el archivo `note.txt` desde Wireshark.

Después de descargarlo, abrí el archivo para visualizar su contenido.


Dentro del archivo se encuentra la información necesaria para responder la consigna, incluyendo el nombre del alienígena.

---

## Qué se aprendió

En este ejercicio aprendí y practiqué:

- Búsqueda de archivos mediante cadenas dentro de una captura.
- Utilización de **Edit > Find Packet**.
- Identificación de referencias a archivos dentro del contenido HTML.
- Diferenciación entre una referencia a un archivo y el archivo realmente transmitido.
- Utilización de **File > Export Objects > HTTP**.
- Filtrado de objetos HTTP por nombre.
- Identificación del paquete que contiene un archivo.
- Extracción de archivos desde una captura de tráfico.