# The Dev Guide — Plan del proyecto

## ¿Qué es?
Repo personal de documentación técnica en GitHub.  
Organizado por **tecnología + versión**, con teoría y práctica.  
Objetivo: aprender mientras se documenta, con código limpio y commits atómicos.

---

## Estructura general del repo

```
the-dev-guide/
  README.md        → portada "THE DEV GUIDE" + badges por tecnología
  CLAUDE.md        → convenciones para Claude Code CLI
  _template.md     → plantilla base de cada tema
  javascript/
  angular/
  react/
  dotnet/
```

---

## Portada (README.md)

- Título centrado: `THE DEV GUIDE`
- Badges clicables por tecnología (shields.io), uno por carpeta

```md
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](./javascript/)
[![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)](./angular/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](./react/)
[![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](./dotnet/)
```

---

## JavaScript — estructura interna

```
javascript/
  README.md        → tarjetas/badges por tema
  fundamentos.md   → tipos, scope, hoisting
  funciones.md     → arrow, callbacks, closures
  arrays.md        → .map, .filter, .shift, .reduce...
  objetos.md
  asincronia.md    → promises, async/await
  librerias.md     → lodash, date-fns (ecosistema)
  ejercicios/
    nivel-1.md
    nivel-2.md
    nivel-3.md
```

### Categorización de métodos de Array

| Categoría | Métodos |
|---|---|
| 🔄 Mutan el array | push, pop, shift, unshift, splice, sort |
| ✨ Devuelven uno nuevo | map, filter, slice, reduce, concat |
| 🔍 Buscan / preguntan | find, includes, some, every, indexOf |

> Esta tabla va dentro de `arrays.md`, no como sección suelta.

---

## Otras tecnologías (Angular, React, .NET)

Misma estructura base por carpeta:

```
angular/
  README.md        → índice de temas
  routing.md
  forms.md
  ...
```

Incluyen sección de cambios por versión, por ejemplo:

```md
## 📌 Cambios por versión
- ⚠️ v11 — RouterModule.forRoot(routes)
- ✅ v17 — provideRouter(routes) (standalone)
```

---

## Plantilla de cada tema (`_template.md`)

````md
# [Tema] — [Tecnología]

> Estado: ✅ · Base: [versión]

## 🧠 Teoría
<details><summary>Ver</summary>
...concepto en pocas líneas...
</details>

## 🛠️ Métodos / Práctica
...código o tabla...

## 📌 Cambios por versión
- ...

## 🔗 Fuente oficial
- [Docs](https://...)
````

> El `<details>` da efecto plegable sin salir de Markdown.  
> Sirve para recuerdo activo: intentas recordar antes de abrir.

---

## Ejercicios

- Banco de retos en Markdown por niveles: `nivel-1.md`, `nivel-2.md`, `nivel-3.md`
- Formato simple: enunciado → espacio para pensar → solución en `<details>`
- **Generador interactivo de retos**: idea válida, pero es una app web → proyecto separado a futuro

---

## Flujo de trabajo y commits

- Un componente / archivo a la vez
- Commits atómicos con prefijos convencionales:

```
feat: crea componente X
docs: agrega arrays.md con métodos
refactor: limpia estructura de funciones.md
```

- Workflow: crear → revisar → commit → siguiente

---

## CLAUDE.md — convenciones para Claude Code

Archivo en la raíz que lleva las convenciones al contexto de Claude Code CLI.  
Incluye: estructura del repo, formato de plantilla, prefijos de commit, criterios de estado (✅ ⚠️ 🔄).

---

## A futuro

- Agentes para formatear otros proyectos usando las convenciones de este repo
- Generador interactivo de ejercicios por nivel (proyecto aparte)
