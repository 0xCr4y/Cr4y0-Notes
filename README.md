# Cr4y0 Notes

Sitio público generado con [Quartz](https://quartz.jzhao.xyz/) a partir de una selección curada de `Obsidian-Apuntes` (repo privado).

URL final una vez desplegado: `https://0xCr4y.github.io/cr4y0-notes`

## Regla de oro

Este repo es **público**. Todo lo que entra a `content/` termina en internet.

**Nunca copies acá:**
- Cualquier cosa de `Trabajo-Cliente/` (EY, NTTDATA) del vault privado — datos reales de clientes.
- Capturas, IPs o flags de exámenes de certificación (OSCP, eWPTX, CRTO, etc.) — viola los términos del examen.
- Credenciales, tokens, claves API, hashes reales.

## Flujo de publicación

1. Trabajas normalmente en el vault privado (`Obsidian-Apuntes`).
2. Cuando una nota está lista para ser pública, la **copias a mano** a `content/` en este repo (manteniendo o no la subcarpeta, como prefieras).
3. Revisas el diff (`git diff`) antes de commitear — es el checkpoint para detectar algo sensible que se coló.
4. `git push` a `main` → GitHub Actions construye y despliega solo a GitHub Pages automáticamente (ver `.github/workflows/deploy.yaml`).

No hay sync automático entre el vault privado y este repo a propósito: cada nota que se publica es una decisión manual.

## Desarrollo local

```bash
npm i
npx quartz build --serve
```

Abre `http://localhost:8080` para previsualizar el sitio antes de publicar.

## Configuración

- `quartz.config.yaml` — título del sitio, tema, plugins, `baseUrl`.
- `content/` — las notas publicadas (Markdown, estilo Obsidian: wikilinks, front matter, etc.).

---

Generado a partir de [Quartz](https://github.com/jackyzha0/quartz) de jackyzha0 (remote `upstream`, para hacer `git pull upstream main` cuando haya actualizaciones).
