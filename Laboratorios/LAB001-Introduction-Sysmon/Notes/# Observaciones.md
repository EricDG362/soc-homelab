# Observaciones

- Sysmon se instaló correctamente utilizando el archivo
  sysmonconfig-export.xml.

- Se verificó la generación de eventos de creación de procesos
  (Event ID 1).

- Se observó que Notepad en Windows 11 se ejecuta desde
  Program Files\WindowsApps y que el proceso padre también
  aparece como Notepad, comportamiento esperado para esta
  versión de Windows.

- Se confirmó que Sysmon está registrando actividad del sistema
  correctamente y está listo para integrarse con Wazuh.