# Pull, Clone y Fetch en GitHub

> Cómo traer código de un repositorio remoto a mi máquina local.

**Última actualización:** 2026-05-12
**Estado:** ✅ Probado

---

## 🎯 ¿Cuándo uso esto?

- **Clone:** cuando es la primera vez que bajo un repo a mi máquina.
- **Pull:** cuando ya tengo el repo y quiero traer los cambios nuevos del remoto.
- **Fetch:** cuando quiero ver qué cambios hay en el remoto sin aplicarlos todavía.

---

## 📋 Pasos

### Clonar un repo por primera vez
```bash
git clone https://github.com/usuario/nombre-repo.git
cd nombre-repo
```
Qué hace: descarga todo el repo (con su historial) a una carpeta nueva.

### Hacer pull (traer cambios)
```bash
git pull origin main
```
Qué hace: trae los commits nuevos de la rama `main` del remoto y los fusiona con tu rama local.

> 💡 Si tu rama se llama distinto (`master`, `develop`), cambia `main` por ese nombre.

### Fetch (ver sin aplicar)
```bash
git fetch origin
git log origin/main --oneline
```
Qué hace: descarga los cambios pero NO los aplica. Útil para revisar antes de mergear.

---

## ⚠️ Errores comunes

### Error: `Your local changes would be overwritten by merge`
**Causa:** tienes cambios sin commitear que chocan con los del remoto.
**Solución (opción 1 - guardar tus cambios):**
```bash
git stash
git pull origin main
git stash pop
```
**Solución (opción 2 - descartar tus cambios):**
```bash
git reset --hard
git pull origin main
```
⚠️ Cuidado: la opción 2 borra tus cambios locales.

### Error: `fatal: refusing to merge unrelated histories`
**Causa:** los dos repos no comparten historial común.
**Solución:**
```bash
git pull origin main --allow-unrelated-histories
```

---

## 💡 Tips personales

- Siempre hacer `git status` antes de un pull para ver si tengo cambios sin commitear.
- Si trabajo en equipo, hacer pull al inicio de cada sesión para no quedarme atrás.
- `git pull --rebase` mantiene el historial más limpio que un pull normal.

---

## 🔗 Fuentes

- [Documentación oficial de git pull](https://git-scm.com/docs/git-pull)
- [Documentación oficial de git clone](https://git-scm.com/docs/git-clone)
- [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/syncing/git-pull)
