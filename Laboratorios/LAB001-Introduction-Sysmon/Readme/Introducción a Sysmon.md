# LAB-001 - Introducción a Sysmon y análisis básico de eventos

## Objetivo

Instalar Sysmon en una máquina virtual con Windows 11 y verificar su funcionamiento mediante la generación y análisis de eventos básicos del sistema.

## Entorno

* Sistema operativo: Windows 11
* Herramienta de monitoreo: Sysmon v15.20
* Configuración utilizada: `sysmonconfig-export.xml`
* Plataforma de virtualización: VirtualBox

## Actividades realizadas

1. Instalación de Sysmon utilizando un archivo de configuración personalizado.
2. Verificación de la correcta instalación del servicio.
3. Apertura del Visor de eventos.
4. Navegación a:

   * Applications and Services Logs
   * Microsoft
   * Windows
   * Sysmon
   * Operational
5. Generación manual de actividad para producir eventos.
6. Ejecución de:

   * `whoami`
   * `ipconfig`
   * `notepad.exe`
7. Creación y apertura del archivo `prueba.txt`.
8. Revisión de los eventos generados por Sysmon.

## Evidencias observadas

Se verificó la generación de eventos relacionados con:

* Creación de procesos (Event ID 1).
* Modificaciones del Registro (Event ID 13).
* Ejecución de aplicaciones del sistema.

Entre los procesos analizados se identificaron:

* `cmd.exe`
* `notepad.exe`
* `SecurityHealthHost.exe`
* `svchost.exe`

## Análisis

Los eventos observados fueron consistentes con la actividad realizada por el usuario durante la práctica.

No se detectaron indicadores de comportamiento malicioso. Las ejecuciones de procesos y modificaciones registradas correspondieron a operaciones legítimas del sistema operativo y acciones iniciadas manualmente.

La práctica permitió comprender cómo Sysmon amplía la visibilidad sobre la actividad interna de Windows y proporciona información útil para investigaciones de seguridad.

## Conclusión

La instalación y configuración de Sysmon fue exitosa.

Se validó la correcta generación de eventos y se realizó una primera aproximación al análisis de telemetría de Windows, sentando las bases para futuras investigaciones utilizando un SIEM como Wazuh y escenarios de ataque más avanzados.
