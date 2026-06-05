# Plan de acción - The Dev Guide

> Guía simple para construir **The Dev Guide** como un repo profesional de documentación técnica.
> Estilo: cavernícola profesional. Sabe mucho. Dice lo necesario. Ejecuta limpio.

**Última actualización:** 2026-06-05  
**Estado:** En proceso  
**Responsable:** Humberto  
**Rol de la IA:** copiloto mínimo, no piloto automático.

---

## 1. Norte del proyecto

**The Dev Guide** será mi guía personal de desarrollo.

El repo se organizará por **tecnología + versión + práctica**.

Debe servir para:

- Aprender mientras documento.
- Recordar teoría sin leer libros enteros otra vez.
- Practicar con ejercicios por nivel.
- Guardar cambios importantes entre versiones.
- Usar IA con reglas claras, sin perder control.
- Trabajar con commits atómicos y orden profesional.

No es blog.  
No es curso gigante.  
No es acumulador de apuntes sueltos.  
Es mi sistema de estudio y consulta técnica.

---

## 2. Decisión base

La conversación original propone esta estructura:

```text
the-dev-guide/
  README.md
  CLAUDE.md
  _template.md
  javascript/
  angular/
  react/
  dotnet/
```

El repo actual ya tiene documentación útil:

```text
01-git/
02-setup/
_templates/
_session-log/
```

Decisión profesional:

- No borrar lo actual.
- Crear la nueva estructura por tecnología.
- Mantener Git/setup como sección de soporte.
- Después decidir si `01-git/` y `02-setup/` se quedan así o migran a `dev-tools/`.

Regla: primero estabilidad, luego orden perfecto.

---

## 3. Estructura objetivo

```text
The-Dev-Guide/
|-- README.md
|-- PLAN-ACCION.md
|-- CLAUDE.md
|-- _template.md
|-- javascript/
|   |-- README.md
|   |-- fundamentos.md
|   |-- funciones.md
|   |-- arrays.md
|   |-- objetos.md
|   |-- asincronia.md
|   |-- librerias.md
|   `-- ejercicios/
|       |-- nivel-1.md
|       |-- nivel-2.md
|       `-- nivel-3.md
|-- angular/
|   |-- README.md
|   |-- routing.md
|   |-- forms.md
|   `-- componentes.md
|-- react/
|   |-- README.md
|   |-- componentes.md
|   |-- hooks.md
|   `-- estado.md
|-- dotnet/
|   |-- README.md
|   |-- fundamentos.md
|   |-- web-api.md
|   `-- entity-framework.md
|-- 01-git/
|-- 02-setup/
|-- _templates/
`-- _session-log/
```

---

## 4. Reglas de documentación

Cada tema debe tener:

- Título claro.
- Estado: probado, por validar o en proceso.
- Versión base cuando aplique.
- Teoría corta.
- Práctica con ejemplos.
- Cambios por versión si importa.
- Fuente oficial.
- Errores comunes si ya los viví.

Formato base:

```md
# [Tema] - [Tecnología]

> Estado: En proceso | Probado | Por validar
> Base: [versión]

## Teoría
<details><summary>Ver</summary>
Explicación corta.
</details>

## Práctica
Código, tabla o pasos.

## Cambios por versión
- v11: forma anterior.
- v17: forma nueva.

## Errores comunes
- Error:
- Causa:
- Solución:

## Fuente oficial
- [Docs](https://...)
```

Regla de oro:

Si el documento no ayuda a estudiar, recordar o ejecutar, se recorta.

---

## 5. Flujo profesional por tarea

Cada avance se trabaja así:

1. Elegir una tarea pequeña.
2. Crear o editar un solo tema principal.
3. Revisar que la estructura tenga sentido.
4. Probar ejemplos si aplica.
5. Actualizar índice del área.
6. Revisar `git status`.
7. Commit atómico.
8. Pasar a la siguiente tarea.

Comandos base:

```powershell
git status
git add .
git commit -m "docs: agrega <tema>"
git push
```

Mensajes válidos:

```text
docs: agrega plan de accion del proyecto
docs: crea estructura base por tecnologias
docs: agrega portada con badges de tecnologias
docs: agrega template base de temas
docs: agrega fundamentos de javascript
docs: agrega guia de arrays en javascript
docs: agrega ejercicios nivel 1 de javascript
docs: agrega convenciones para claude code
```

Regla:

Un commit = una intención cerrada.

---

## 6. Backlog por fases

### Fase 0 - Registrar contexto

Objetivo: dejar claro qué se va a construir y por qué.

- [x] Guardar conversación base en `the-dev-guide-plan.md`.
- [x] Crear `PLAN-ACCION.md`.
- [ ] Revisar el plan y ajustar si falta algo.
- [ ] Commit: `docs: agrega plan de accion del proyecto`.

### Fase 1 - Portada profesional

Objetivo: que `README.md` funcione como entrada principal del proyecto.

Tareas:

- [ ] Título centrado: `THE DEV GUIDE`.
- [ ] Descripción corta del repo.
- [ ] Badges clicables por tecnología.
- [ ] Links a carpetas principales.
- [ ] Sección corta: cómo usar este repo.
- [ ] Commit: `docs: actualiza portada principal`.

Badges base:

```md
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](./javascript/)
[![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)](./angular/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](./react/)
[![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](./dotnet/)
```

### Fase 2 - Plantilla base

Objetivo: que todos los temas se documenten igual.

Tareas:

- [ ] Crear `_template.md` en la raíz.
- [ ] Decidir si `_templates/plantilla-doc.md` se mantiene o se reemplaza.
- [ ] Incluir secciones: teoría, práctica, versiones, errores, fuente.
- [ ] Commit: `docs: agrega template base de temas`.

### Fase 3 - Convenciones para IA

Objetivo: crear el agente especializado en mi forma de trabajar.

Tareas:

- [ ] Crear `CLAUDE.md`.
- [ ] Incluir estructura del repo.
- [ ] Incluir reglas de documentación.
- [ ] Incluir flujo de commits.
- [ ] Incluir qué puede y qué no puede hacer la IA.
- [ ] Commit: `docs: agrega convenciones para claude code`.

### Fase 4 - JavaScript base

Objetivo: crear la primera tecnología completa.

Tareas:

- [ ] Crear carpeta `javascript/`.
- [ ] Crear `javascript/README.md`.
- [ ] Crear `javascript/fundamentos.md`.
- [ ] Crear `javascript/funciones.md`.
- [ ] Crear `javascript/arrays.md`.
- [ ] Crear `javascript/objetos.md`.
- [ ] Crear `javascript/asincronia.md`.
- [ ] Crear `javascript/librerias.md`.
- [ ] Crear `javascript/ejercicios/nivel-1.md`.
- [ ] Crear `javascript/ejercicios/nivel-2.md`.
- [ ] Crear `javascript/ejercicios/nivel-3.md`.

Commits sugeridos:

```text
docs: crea estructura de javascript
docs: agrega fundamentos de javascript
docs: agrega guia de funciones javascript
docs: agrega guia de arrays javascript
docs: agrega ejercicios iniciales de javascript
```

Tabla obligatoria para `javascript/arrays.md`:

| Categoría | Métodos |
|---|---|
| Mutan el array | `push`, `pop`, `shift`, `unshift`, `splice`, `sort` |
| Devuelven uno nuevo | `map`, `filter`, `slice`, `reduce`, `concat` |
| Buscan o preguntan | `find`, `includes`, `some`, `every`, `indexOf` |

### Fase 5 - Angular

Objetivo: documentar Angular con foco en versiones.

Tareas:

- [ ] Crear carpeta `angular/`.
- [ ] Crear `angular/README.md`.
- [ ] Crear `angular/routing.md`.
- [ ] Crear `angular/forms.md`.
- [ ] Crear `angular/componentes.md`.
- [ ] Agregar cambios por versión cuando aplique.
- [ ] Commit: `docs: crea estructura de angular`.

Ejemplo de versiones:

```md
## Cambios por versión
- v11: `RouterModule.forRoot(routes)`
- v17: `provideRouter(routes)` con standalone
```

### Fase 6 - React

Objetivo: documentar React con teoría mínima y práctica clara.

Tareas:

- [ ] Crear carpeta `react/`.
- [ ] Crear `react/README.md`.
- [ ] Crear `react/componentes.md`.
- [ ] Crear `react/hooks.md`.
- [ ] Crear `react/estado.md`.
- [ ] Commit: `docs: crea estructura de react`.

### Fase 7 - .NET

Objetivo: documentar base de .NET para proyectos backend.

Tareas:

- [ ] Crear carpeta `dotnet/`.
- [ ] Crear `dotnet/README.md`.
- [ ] Crear `dotnet/fundamentos.md`.
- [ ] Crear `dotnet/web-api.md`.
- [ ] Crear `dotnet/entity-framework.md`.
- [ ] Commit: `docs: crea estructura de dotnet`.

### Fase 8 - Ejercicios y práctica

Objetivo: estudiar de forma activa.

Regla de ejercicios:

- Enunciado primero.
- Espacio para pensar.
- Solución oculta con `<details>`.
- Nivel claro.

Formato:

```md
## Reto 1 - Nombre

Enunciado corto.

<details><summary>Solución</summary>

```js
// solución
```

</details>
```

Commit: `docs: agrega banco inicial de ejercicios`.

### Fase 9 - Proyecto futuro separado

Objetivo: no mezclar documentación con app.

Idea futura:

- Generador interactivo de retos por nivel.
- Web app aparte.
- Este repo solo puede guardar la especificación inicial.

Commit si se documenta:

```text
docs: registra idea de generador de ejercicios
```

---

## 7. Registro de dependencias

Este repo casi no debe tener dependencias porque es documentación.

Si una dependencia aparece, se registra así:

| Fecha | Dependencia | Tipo | Comando | Para qué sirve | Commit |
|---|---|---|---|---|---|
| YYYY-MM-DD | paquete | prod/dev/tool | `comando` | razón corta | mensaje |

Regla:

Si no puedo explicar una dependencia en una frase, no la instalo.

---

## 8. Cuando me trabe

Plantilla rápida:

```text
Objetivo:

Dónde me trabé:

Archivo:

Comando o paso:

Error exacto:

Qué esperaba:

Qué ya intenté:
```

Prompt para IA:

```text
Estoy trabajando en The Dev Guide.

Objetivo:
<una frase>

Me trabé aquí:
<paso exacto>

Error o duda:
<texto exacto>

Restricción:
No programes por mí. Dame pasos concretos, dime qué verificar y explica solo lo necesario.
```

---

## 9. Reglas para la IA

La IA puede:

- Ordenar notas.
- Crear checklists.
- Convertir conversación en backlog.
- Sugerir estructura.
- Revisar consistencia.
- Sugerir commits.
- Explicar corto.

La IA no debe:

- Borrar archivos sin permiso.
- Hacer commits sin revisión.
- Instalar dependencias sin razón.
- Inventar carpetas fuera del plan.
- Escribir relleno.
- Hacer el trabajo sin que yo entienda.

Prompt base para `CLAUDE.md`:

```text
Actúa como copiloto técnico para The Dev Guide.

Prioridad:
1. Claridad.
2. Estructura.
3. Pasos exactos.
4. Commits atómicos.
5. Mínimo texto necesario.

Reglas:
- Lee README.md y PLAN-ACCION.md antes de proponer cambios.
- Respeta la estructura por tecnología.
- Un tema por archivo.
- Usa la plantilla base.
- Si algo no está probado, marca "por validar".
- Si creas archivo nuevo, sugiere actualizar el índice correspondiente.
- Antes de commit, pide revisar diff.
```

---

## 10. Checklist de cierre de sesión

Antes de cerrar:

- [ ] Revisé `git status`.
- [ ] Sé qué archivos cambiaron.
- [ ] Actualicé índices si agregué archivos.
- [ ] Registré aprendizaje si fue importante.
- [ ] Hice commit si la tarea terminó.
- [ ] Dejé claro el siguiente paso.

Si no hago commit:

```text
No hice commit porque:
<razón>
```

---

## 11. Siguiente paso recomendado

Hacer la Fase 0 completa:

1. Revisar este archivo.
2. Ajustar lo que no encaje con tu intención.
3. Hacer commit:

```powershell
git status
git add PLAN-ACCION.md the-dev-guide-plan.md
git commit -m "docs: agrega plan de accion del proyecto"
```

Después seguir con Fase 1: portada `README.md`.
