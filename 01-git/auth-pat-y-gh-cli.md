# Autenticación con GitHub: PAT y GitHub CLI

> Cómo autenticarte para hacer `git push` a un repo de GitHub usando un Personal Access Token (PAT) o el GitHub CLI (`gh`). GitHub ya no acepta password normal desde 2021 — necesitas una de estas dos.

**Última actualización:** 2026-05-12
**Estado:** ✅ Probado (PAT) · ✅ Probado (gh CLI)

---

## 🎯 ¿Cuándo uso esto?

- Primera vez que hago `push` a un repo nuevo en GitHub desde una máquina.
- Cambié de máquina y necesito reconfigurar credenciales.
- Mi PAT expiró y `git push` empezó a fallar con `403` o pidiendo password.

> 💡 Regla general: usa **`gh` CLI** si vas a trabajar seguido con GitHub (es más cómodo). Usa **PAT directo** si solo quieres pushear rápido y no quieres instalar nada.

---

## 📋 Opción A — Personal Access Token (PAT)

### 1. Generar el token en GitHub

1. Ir a https://github.com/settings/tokens
2. Click en **"Generate new token (classic)"** (o **"Fine-grained tokens"** para más control).
3. Ponerle:
   - **Note:** algo descriptivo, ej. `laptop-personal`
   - **Expiration:** 90 días o más (sin "no expiration" por seguridad).
   - **Scopes mínimos para push a repos:** solo marca `repo` (eso cubre push/pull a repos públicos y privados).
4. Click en **"Generate token"**.
5. **Copia el token inmediatamente** — GitHub solo te lo muestra una vez.

> ⚠️ El token es como una contraseña. No lo subas a ningún repo, no lo pegues en chats públicos.

### 2. Usarlo al hacer push

La primera vez que pusheas, Git te pide credenciales:

```powershell
git push -u origin main
# Username for 'https://github.com': tu-usuario-github
# Password for 'https://tu-usuario@github.com': PEGAR_EL_TOKEN_AQUI
```

Como **password pegas el token**, no tu contraseña real de GitHub.

### 3. Guardar el token para no pegarlo cada vez

En Windows, Git ya usa el **Credential Manager** por defecto. Después del primer push exitoso, queda guardado. Para verificar:

```powershell
git config --global credential.helper
# debería responder: manager (o manager-core)
```

Si quieres borrarlo después (ej. cuando el token expire):
- Panel de control → Administrador de credenciales → Credenciales de Windows → buscar `git:https://github.com` y eliminar.

---

## 📋 Opción B — GitHub CLI (`gh`)

### 1. Instalar `gh`

Windows (con winget):
```powershell
winget install --id GitHub.cli
```

Verificar:
```powershell
gh --version
```

### 2. Autenticarse

```powershell
gh auth login
```

Te hace varias preguntas:
- **What account?** → `GitHub.com`
- **Protocol?** → `HTTPS` (recomendado)
- **Authenticate Git with GitHub credentials?** → `Yes` (esto es la magia, configura Git automáticamente)
- **How to authenticate?** → `Login with a web browser` (más fácil) o pegar un PAT.

Si eliges navegador, te da un código tipo `XXXX-XXXX`, abres el navegador y lo pegas. Listo.

### 3. Verificar

```powershell
gh auth status
```

Debería mostrar que estás autenticado y que Git va a usar `gh` como credential helper.

### 4. Bonus: crear repos desde la terminal

Ya que tienes `gh`, no necesitas ir a github.com a crear repos:

```powershell
gh repo create The-Dev-Guide --public --source=. --remote=origin --push
```

Eso crea el repo en GitHub, lo conecta como `origin`, y hace push inicial — todo en un comando.

---

## ⚠️ Errores comunes

### Error: `remote: Support for password authentication was removed on August 13, 2021.`
**Causa:** estás intentando autenticarte con tu password real de GitHub. Ya no funciona.
**Solución:** generar un PAT (Opción A) o usar `gh auth login` (Opción B).

### Error: `remote: Permission to user/repo.git denied to otro-user.`
**Causa:** Git está usando credenciales de otro usuario guardadas en el Credential Manager.
**Solución:** abre Administrador de credenciales de Windows, borra la entrada de `git:https://github.com`, y vuelve a pushear (te pedirá credenciales de nuevo).

### Error: `src refspec main does not match any`
**Causa:** la rama `main` aún no tiene commits. Suena a auth pero no lo es.
**Solución:**
```powershell
git add .
git commit -m "Initial commit"
git push -u origin main
```

### El token expiró
**Solución:** generar uno nuevo en https://github.com/settings/tokens y borrar el viejo del Credential Manager para que Git pida el nuevo en el próximo push.

---

## 💡 Tips personales

- Permisos **mínimos** en el PAT — solo `repo`. No le des `delete_repo`, `admin:org`, etc. salvo que de verdad los necesites.
- Si vas a usar este repo seguido, vale la pena instalar `gh`: te ahorra el dolor de regenerar PATs cada vez que expiran.
- `gh repo view --web` abre el repo actual en el navegador, útil cuando andas en la terminal y necesitas ver issues/PRs.
- Para revocar acceso rápido: borra el PAT en GitHub → Settings → Developer settings → Tokens. Inmediato.

---

## 🔗 Fuentes

- [Creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
- [About authentication to GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)
- [GitHub CLI manual](https://cli.github.com/manual/)
- [gh auth login](https://cli.github.com/manual/gh_auth_login)
