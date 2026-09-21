````
##  Alerta: — Manipulación de EDR mediante EDR-Freeze

##  Descripción

Investigación de un intento de manipulación de las defensas de seguridad de un endpoint mediante **EDR-Freeze**, después de que un atacante obtuviera acceso al sistema mediante un ataque de fuerza bruta.

Durante la investigación se identificó la descarga y ejecución de un archivo `.exe` obtenido desde GitHub, cuyo objetivo era interferir con el funcionamiento del mecanismo de protección del endpoint y suspender las capacidades de detección de Microsoft Defender.



#  Investigación

## 1. Análisis del hash del archivo

Como primer paso se analizó el **hash proporcionado por la alerta** utilizando VirusTotal.

El análisis mostró que el archivo era detectado como malicioso por múltiples motores de seguridad. En total, **54 motores lo clasificaron como malicioso**.

Este resultado aportó evidencia adicional de que el archivo analizado no correspondía a un ejecutable legítimo.

> **Ver Imagen 1:** Captura de VirusTotal

---

## 2. Identificación del endpoint comprometido

Desde **Security Endpoint** se accedió al host afectado:

**Host:** `ws-prod-02`

Durante el análisis se identificaron procesos relacionados con la ejecución del archivo malicioso.

Los registros mostraron la creación de procesos y permitieron observar que el ejecutable fue iniciado mediante:

`PowerShell.exe`

> **Ver Imagen 2:** Captura de Security Endpoint

---

## 3. Análisis directo del host

Posteriormente se accedió al equipo afectado para realizar un análisis más detallado.

En la carpeta **Downloads** todavía se encontraba el ejecutable relacionado con **EDR-Freeze**, lo que permitió confirmar que el archivo analizado había sido descargado y permanecía almacenado en el endpoint.

> **Ver Imagen 3:** Carpeta `Download`.

### Clasificación inicial

Con la evidencia recopilada hasta este punto, la alerta puede clasificarse como un **Verdadero Positivo (True Positive)** y requiere continuar con un análisis más profundo para determinar el alcance de la actividad y las acciones realizadas por el atacante.

---

# 4. Investigación del acceso inicial

Como antecedente de la alerta, el analista L1 informó que previamente se había detectado un acceso al sistema mediante un ataque de **fuerza bruta**.

Para investigar esta actividad se revisaron los registros de autenticación del sistema.

Entre las **06:59 y las 07:00** se identificaron cinco intentos de inicio de sesión:

- 4 eventos **Event ID 4625** — inicio de sesión fallido.
- 1 evento **Event ID 4624** — inicio de sesión exitoso.

A partir del evento de autenticación exitoso se identificó como dirección IP de origen:

`212.8.243.56`

La secuencia observada es consistente con un ataque de fuerza bruta que finalmente consiguió credenciales válidas.

> **Ver Imagen 4:**eventos 4625 y 4624.


---

# 5. Análisis mediante Event Viewer

Para realizar un análisis más profundo de la actividad ejecutada en el endpoint se accedió a:

**Windows → Event Viewer → Applications and Services Logs**

También se revisaron los registros generados por **Sysmon**.

El objetivo fue correlacionar diferentes tipos de eventos y reconstruir la actividad realizada por el ejecutable.

Se analizaron principalmente:

| Event ID | Actividad |
|---|---|
| **1** | Process Creation |
| **3** | Network Connection |
| **11** | File Create |
| **22** | DNS Query |

La correlación de estos eventos permitió obtener información adicional sobre la ejecución del malware, sus conexiones de red, consultas DNS y archivos creados durante la actividad.

> **Ver Imagen 5:** Event Viewer mostrando los eventos

# 6. Análisis de la ejecución del malware

Durante el análisis de los eventos de Sysmon se identificó la creación de un proceso hijo:

`WerFaultSecure.exe`

Este ejecutable corresponde a un componente legítimo de Windows relacionado con **Windows Error Reporting**.

Sin embargo, el proceso fue ejecutado con parámetros específicos que dirigían su actividad hacia otro proceso:

```text
/h /pid 6080 /tid 6076 ...
````

La utilización de un binario legítimo de Windows en este contexto es consistente con una técnica de **Living off the Land (LotL)**, donde un atacante abusa de componentes existentes y confiables del sistema para realizar acciones maliciosas.

En este caso, la actividad observada indica que el atacante intentó utilizar `WerFaultSecure.exe` para interactuar con un proceso protegido asociado a Microsoft Defender.

---

# 7. Manipulación de Microsoft Defender

La actividad observada es consistente con un intento de **evadir o deshabilitar las protecciones del endpoint** para impedir que el EDR/Defender detectara las acciones posteriores del atacante.

---

# Contención

Con base en la evidencia recopilada durante la investigación, existe evidencia suficiente para considerar que el endpoint **`ws-prod-02` fue comprometido** y que un actor obtuvo acceso al sistema y posteriormente ejecutó una herramienta destinada a interferir con las defensas de seguridad.

Como medida de contención se recomienda:

* **Aislar inmediatamente el endpoint de la red.**
* Evitar que el atacante pueda acceder a otros sistemas o recursos internos.
* Preservar los registros y evidencias antes de realizar modificaciones innecesarias.
* Revisar otros endpoints que hayan podido comunicarse con el equipo comprometido.
* Investigar la actividad de la IP `212.8.243.56`.
* Revisar las credenciales utilizadas durante el acceso.
* Considerar el restablecimiento de las credenciales comprometidas.

---

# Acciones de remediación

Una vez finalizada la adquisición y preservación de evidencias, se recomienda:

* Eliminar el ejecutable malicioso `EDR-Freeze`.
* Eliminar archivos y componentes asociados a la herramienta maliciosa.
* Verificar que Microsoft Defender y las protecciones del endpoint vuelvan a estar activas.
* Revisar configuraciones de seguridad que hayan sido modificadas.
* Restablecer las credenciales utilizadas durante el compromiso.
* Analizar persistencia y posibles mecanismos utilizados para mantener el acceso.
* Revisar otros equipos en busca de indicadores relacionados.
* Mantener el aislamiento hasta completar la investigación y validar la integridad del sistema.

