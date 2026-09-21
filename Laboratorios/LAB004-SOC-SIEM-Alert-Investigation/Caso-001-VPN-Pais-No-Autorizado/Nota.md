##  Alerta: Conexión VPN detectada desde un país no autorizado


**Tipo:** Acceso VPN sospechoso

---

## Investigación

### 1. Identificación de la IP de origen

Como primera medida, se identifica la **IP de origen (Source IP)** asociada a la solicitud sospechosa.

>  **Ver Imagen 1:** IP de origen.

---

### 2. Análisis de los registros del Proxy

Al analizar los registros en bruto del Proxy, se observa que la petición recibió:

```text
Status = 200
````

Este código indica que la solicitud HTTP fue procesada correctamente.

Sin embargo, esto **no significa que el usuario haya conseguido autenticarse correctamente**. En este punto solamente sabemos que la solicitud llegó al servicio y fue procesada.

Por lo tanto, es necesario continuar investigando para determinar si el atacante consiguió autenticarse con las credenciales de Mónica.

>  **Ver Imagen 2:** Proxy `Status=200`.

---

### 3. Investigación de la dirección IP

La dirección IP de origen es investigada mediante herramientas de inteligencia y reputación como **VirusTotal** y **WHOIS**.

La información obtenida permite determinar que la dirección IP se encuentra geolocalizada en **Vietnam**, un país que no se encuentra entre las ubicaciones autorizadas para este acceso.

Esto confirma que la actividad coincide con la condición de la regla de detección y permite clasificar la alerta como un **Verdadero Positivo (True Positive)**.

>  **Ver Imagen 3:** VirusTotal mostrando la geolocalización de la IP en Vietnam.

---

### 4. Análisis de reputación de la IP

También se realiza una consulta de la dirección IP en **AbuseIPDB** para analizar su reputación y comprobar si existen reportes relacionados con actividades maliciosas.

La IP presenta una reputación negativa y ha sido reportada por diferentes fuentes en distintos momentos.

Entre las categorías de actividad reportadas se encuentran:

* Fuerza Bruta (Brute Force)
* Ataques Web
* Actividad Maliciosa

La información obtenida de VirusTotal y AbuseIPDB aporta contexto adicional sobre la dirección IP y aumenta el nivel de sospecha de la actividad observada.

>  **Ver Imagen 4:** AbuseIPDB mostrando los reportes asociados a la dirección IP.

---

##  ¿El atacante consiguió acceder?

Después de determinar que la conexión provenía de una ubicación no autorizada, el siguiente paso consiste en determinar si el atacante logró autenticarse correctamente.

### 5. Análisis del proceso de autenticación y MFA

Al analizar nuevamente los registros del Proxy, se observa que posteriormente se generó y envió un **OTP (One-Time Password)**.

Esto indica que las credenciales proporcionadas fueron suficientes para avanzar hasta la etapa de autenticación multifactor.

>  **Ver Imagen 5:** Envío del OTP.

---

### 6. Análisis del correo electrónico de MFA

Los detalles del correo electrónico contienen información relacionada con el intento de autenticación, incluyendo:

* OTP generado.
* Dirección IP desde la cual se realizó el intento.
* Información relacionada con la solicitud de autenticación.

Es posible consultar los correos enviados a:

```text
monica[@]letsdefend[.]io
```

mediante la sección **Seguridad de Correo**, con el objetivo de verificar si Mónica recibió el código OTP.

> 📸 **Ver Imagen 6:** Correo electrónico con el OTP y los datos asociados al intento de autenticación.

---

### 7. Resultado de la autenticación MFA

El código OTP introducido por el atacante fue **incorrecto**.

Por lo tanto, aunque el atacante aparentemente conocía la contraseña correcta de la cuenta, **no consiguió superar el segundo factor de autenticación (MFA)**.

Como consecuencia:

La evidencia disponible indica que el atacante **no consiguió acceder a la VPN ni al entorno interno mediante este intento**.

---

#  Contención

Debido a que la contraseña de la cuenta fue utilizada correctamente por un tercero, se considera que las credenciales de Mónica podrían estar comprometidas.

Las medidas de contención recomendadas son:

* Restablecer la contraseña de la cuenta de Mónica.
* Verificar que la nueva contraseña no haya sido reutilizada en otros servicios.
* Mantener habilitado el MFA.
* Revisar otros intentos de autenticación asociados a la cuenta.
* No se requiere aislar el equipo en este caso, ya que no existe evidencia de que el atacante haya superado MFA u obtenido acceso a la VPN.

---

#  Lecciones aprendidas

A partir de la investigación se identifican las siguientes medidas preventivas:

* Implementar controles de acceso basados en país o ubicación cuando sean apropiados para el entorno.
* Evitar la reutilización de contraseñas en diferentes plataformas.
* Aplicar políticas de contraseñas robustas.
* Implementar mecanismos de bloqueo o limitación de intentos de autenticación.
* Mantener habilitado MFA como una capa adicional de protección.
* Monitorizar los intentos de autenticación desde ubicaciones inusuales o no autorizadas.

---

#  Conclusión del análisis

La investigación determinó que una cuenta asociada a la usuaria **Mónica** fue utilizada desde una dirección IP geolocalizada en **Vietnam**, una ubicación no autorizada según la regla de detección.

La dirección IP presentó además reportes de actividad sospechosa en fuentes de reputación como VirusTotal y AbuseIPDB.

El análisis de los eventos de autenticación permitió determinar que el atacante aparentemente disponía de la contraseña correcta, ya que consiguió avanzar hasta la etapa de MFA y provocar el envío de un OTP.

Sin embargo, el código OTP introducido fue incorrecto, por lo que **MFA impidió que el atacante obtuviera acceso a la VPN**.

### Clasificación final

**Verdadero Positivo (True Positive)**