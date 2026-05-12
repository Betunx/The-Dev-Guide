# Instalar dependencias en un proyecto Node existente

> Cómo instalar las dependencias de un proyecto Node.js que ya está hecho (clonado de GitHub, descargado, o recibido de alguien más).

**Última actualización:** 2026-05-12
**Estado:** ✅ Probado

---

## 🎯 ¿Cuándo uso esto?

- Cuando clono un repo de Node, React, Angular, Next, Express, etc. y necesito instalarle las dependencias antes de poder correrlo.
- Cuando alguien me pasa un proyecto comprimido y no tiene la carpeta `node_modules`.
- Cuando borré `node_modules` para arreglar algo raro y necesito reinstalar todo.

> 💡 Regla general: si ves un archivo `package.json` en la raíz, necesitas correr algún `install`.

---

## 📋 Casos según el tipo de proyecto

### Caso 1: Proyecto simple (un solo `package.json`)

Estructura típica:
```
mi-proyecto/
├── package.json
├── src/
└── ...
```

Comando:
```bash
npm install
```

O su forma corta:
```bash
npm i
```

Esto crea la carpeta `node_modules/` y descarga todo lo que aparece en `dependencies` y `devDependencies` del `package.json`.

---

### Caso 2: Proyecto con frontend y backend separados (monorepo manual)

Estructura típica:
```
mi-proyecto/
├── package.json          ← raíz (a veces)
├── backend/
│   └── package.json
└── frontend/  (o el nombre que sea, ej. geriaCare)
    └── package.json
```

Tienes que instalar **en cada carpeta** que tenga su propio `package.json`:

```powershell
npm install
npm --prefix backend install
npm --prefix frontend install
```

Qué hace `--prefix`: le dice a npm "ejecuta el install pero usando esta carpeta como si fuera la raíz". Así no tienes que hacer `cd` a cada una.

**Equivalente con `cd` (más verboso pero más claro):**
```bash
cd backend
npm install
cd ..
cd frontend
npm install
cd ..
```

---

### Caso 3: Proyecto con script `install:all` ya configurado

Si el proyecto tiene un `package.json` en la raíz con algo así:

```json
{
  "scripts": {
    "install:all": "npm install && npm --prefix backend install && npm --prefix frontend install"
  }
}
```

Entonces solo necesitas:
```bash
npm run install:all
```

> 💡 Revisa siempre el `package.json` de la raíz para ver qué scripts tiene el proyecto antes de hacerlo a mano. A veces el dev ya dejó atajos.

---

### Caso 4: Monorepo con workspaces (npm/yarn/pnpm)

Si en la raíz del `package.json` ves algo así:
```json
{
  "workspaces": ["backend", "frontend", "packages/*"]
}
```

Solo necesitas un comando desde la raíz:
```bash
npm install
```

npm detecta los workspaces automáticamente e instala todo en una sola pasada.

---

### Caso 5: Usando otros gestores (yarn, pnpm, bun)

Revisa qué archivo de lock tiene el proyecto:

| Archivo lock        | Gestor a usar      | Comando             |
|---------------------|--------------------|---------------------|
| `package-lock.json` | npm                | `npm install`       |
| `yarn.lock`         | yarn               | `yarn install`      |
| `pnpm-lock.yaml`    | pnpm               | `pnpm install`      |
| `bun.lockb`         | bun                | `bun install`       |

> ⚠️ **Importante:** no mezcles gestores en el mismo proyecto. Si tiene `yarn.lock`, no uses `npm install` porque puede romper las versiones.

---

## ⚠️ Errores comunes

### Error: `npm ERR! code ENOENT` / `package.json not found`
**Causa:** estás corriendo `npm install` en una carpeta que no tiene `package.json`.
**Solución:** verifica que estás en la carpeta correcta con `ls` (o `dir` en PowerShell).

### Error: `EACCES: permission denied`
**Causa:** problema de permisos (típico en Linux/Mac).
**Solución:** NO uses `sudo`. Mejor arregla los permisos del directorio o usa `nvm` para manejar Node.

### Error: versiones incompatibles de Node
**Causa:** el proyecto requiere una versión de Node distinta a la que tienes.
**Solución:** revisa el campo `"engines"` del `package.json` y usa [nvm](https://github.com/nvm-sh/nvm) para cambiar de versión:
```bash
nvm install 20
nvm use 20
```

### Error: `node_modules` corrupto o cosas raras pasan
**Solución nuclear (borrar y reinstalar):**
```powershell
# Windows PowerShell
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json
npm install
```
```bash
# Linux/Mac
rm -rf node_modules package-lock.json
npm install
```

---

## 💡 Tips personales

- **Siempre revisa el README** del proyecto antes. Muchos devs ya documentan el comando exacto a usar.
- Si el proyecto tiene `backend` y `frontend`, normalmente necesitas instalar en ambos **antes** de correr nada.
- Usar `npm ci` en lugar de `npm install` es más rápido y confiable cuando el `package-lock.json` ya existe (instala exactamente lo que dice el lock, sin actualizar).
- Si ves muchas advertencias de `deprecated`, generalmente puedes ignorarlas mientras el proyecto compile.
- Para no esperar tanto: `npm install --prefer-offline` reusa el caché si ya instalaste algo antes.

---

## 🔗 Fuentes

- [Documentación oficial de npm install](https://docs.npmjs.com/cli/v10/commands/npm-install)
- [npm workspaces](https://docs.npmjs.com/cli/v10/using-npm/workspaces)
- [Diferencia entre npm install y npm ci](https://docs.npmjs.com/cli/v10/commands/npm-ci)
