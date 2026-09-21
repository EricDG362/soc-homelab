# LAB-001 - Efecto del Firewall de Windows sobre un escaneo Nmap

Objetivo:
Analizar cómo el Firewall de Windows afecta los resultados obtenidos mediante Nmap.

Entorno:
- Kali Linux
- Windows 11
- VirtualBox Host-Only

Prueba 1:
Firewall activado.

Resultado:
Todos los puertos aparecieron como "filtered".

Prueba 2:
Firewall desactivado temporalmente mediante:

netsh advfirewall set allprofiles state off

Resultado:
Nmap detectó:

135/tcp open msrpc
139/tcp open netbios-ssn
445/tcp open microsoft-ds

Conclusión:
El Firewall de Windows estaba filtrando las conexiones entrantes y ocultando los servicios que realmente estaban escuchando en el sistema.