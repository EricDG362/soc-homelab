# LAB-003 - ICMP Flooding Attack

## Técnica

ICMP Flood

---

## Objetivo

Comprender el funcionamiento de un ataque ICMP Flood y aprender a identificarlo mediante Wireshark analizando el tráfico generado entre un atacante y una víctima.

---

## Entorno

- Kali Linux (Atacante)
- Metasploitable2 (Víctima)
- VirtualBox
- Wireshark

---

## Herramientas utilizadas

- hping3
- Wireshark

---

## Escenario

Desde la máquina Kali Linux se generó un gran volumen de paquetes ICMP utilizando **hping3** para simular un ataque de denegación de servicio (DoS).

Se utilizó el parámetro **-a** para falsificar (spoofear) la dirección IP de origen de los paquetes, haciendo que la víctima observe una IP diferente a la del verdadero atacante.

---

## Comando utilizado

```bash
sudo hping3 --icmp --flood -a 10.0.2.100 10.0.2.5
```

---

## Análisis en Wireshark

### Filtro básico

```text
icmp && ip.dst == <IP_víctima> && icmp.type == 8
```

Este filtro permite visualizar únicamente las solicitudes **ICMP Echo Request** dirigidas a la máquina objetivo.

---

## Evidencias observadas

- Gran cantidad de paquetes ICMP en un corto intervalo de tiempo.
- Incremento considerable del tráfico ICMP.
- Flujo continuo de paquetes hacia la misma dirección IP.

En **Statistics → Conversations** se observa que la comunicación entre el origen y el destino concentra una gran cantidad de paquetes, lo que constituye un fuerte indicio de un ataque de inundación.

---

## Consideraciones sobre IP Spoofing

Wireshark **no puede determinar automáticamente** si una dirección IP fue falsificada.

Para obtener indicios de IP Spoofing es posible comparar:

- La dirección MAC asociada a una IP mediante paquetes ARP.
- La dirección MAC que realmente origina los paquetes ICMP.

Si una misma dirección IP aparece asociada a diferentes direcciones MAC, o la MAC observada en el tráfico no coincide con la esperada para esa IP, puede tratarse de un indicio de suplantación de identidad (IP Spoofing). Sin embargo, esta evidencia debe confirmarse correlacionándola con otras fuentes (ARP, tablas del switch, DHCP, firewall, etc.).
