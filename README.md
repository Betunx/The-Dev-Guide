# 🛠️ The Dev Guide

> Manual personal de supervivencia como desarrollador. Comandos, herramientas y métodos que uso en mi día a día. Pensado para consultar rápido cuando no me acuerdo cómo hacer X cosa, y para crecer a lo largo del tiempo.

**Última actualización:** 2026-05-12

---

## 🗂️ Índice

### 01 · Git & GitHub
- [Pull, clone y fetch](./01-git/pull-clone-fetch.md)
- [Autenticación: PAT y GitHub CLI](./01-git/auth-pat-y-gh-cli.md)

### 02 · Setup de proyectos
- [Instalar dependencias en proyecto Node](./02-setup/instalar-dependencias-node.md)

### Próximas secciones (placeholders)
- `03-run/` — cómo correr proyectos (React, Angular, Next, Python…)
- `04-deploy/` — Vercel, Netlify, Railway, Docker básico
- `05-database/` — Postgres local, MongoDB, conexiones
- `06-debugging/` — errores comunes y herramientas
- `07-terminal/` — Bash, PowerShell, atajos
- `99-recursos/` — links, extensiones, cheatsheets

---

## 📝 Cómo uso este repo

1. **Cuando aprendo algo nuevo:** lo documento aquí inmediatamente, aunque sea en bruto. Uso [`_templates/plantilla-doc.md`](./_templates/plantilla-doc.md) como base.
2. **Cuando me atoro:** vengo aquí primero antes de googlear.
3. **Al final de cada sesión de programación:** reviso [`_session-log/`](./_session-log/README.md) para capturar lo nuevo que aprendí esa sesión (manualmente o con ayuda de Claude Code).

### Cada doc debe tener
- Comando o pasos exactos
- Explicación corta de qué hace
- Link a la documentación oficial
- Errores comunes que me han pasado y cómo los resolví

### Convenciones
- Comandos en bloques con su lenguaje (` ```bash `, ` ```powershell `, ` ```javascript `).
- Siempre incluir la fuente al final.
- ✅ probado · ⚠️ por validar · 🔄 en proceso
- Fechas en formato `YYYY-MM-DD`.

---

## 🚀 Flujo de captura rápida (fin de sesión)

Al final de una sesión de programación, en 2-3 minutos:

1. Abrir [`_session-log/README.md`](./_session-log/README.md) y anotar bullets crudos de lo aprendido (comandos, tecnos nuevas, errores resueltos).
2. Si algo merece su propio doc, copiar [`_templates/plantilla-doc.md`](./_templates/plantilla-doc.md) a la carpeta correspondiente.
3. Commit con mensaje descriptivo:
   ```bash
   git add .
   git commit -m "docs: agrega <tema> y notas de sesión YYYY-MM-DD"
   git push
   ```

> 💡 Si trabajo con Claude Code, le pido al final: *"organiza lo que aprendí hoy en el repo según las convenciones"* y revisa el diff antes de commit.
