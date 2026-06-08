# Plan de acción - The Dev Guide

> Plan vivo para construir una guía técnica personal, útil para estudiar y
> consultar durante proyectos reales.

- **Última actualización:** 2026-06-08
- **Estado:** En proceso
- **Responsable:** Humberto
- **Rol de la IA:** explicar, organizar y editar sin reemplazar el aprendizaje.

## 1. Objetivo

The Dev Guide debe permitir:

- aprender conceptos con contexto;
- recordar teoría sin releer documentación completa;
- practicar mediante ejemplos y ejercicios;
- conectar conocimientos de distintas tecnologías;
- conservar errores reales y sus soluciones;
- colaborar con distintas IAs usando las mismas reglas.

## 2. Decisiones vigentes

- `AGENTS.md` es la fuente de verdad para cualquier IA.
- `CLAUDE.md` apunta a `AGENTS.md` para mantener compatibilidad con Claude.
- El conocimiento se clasifica por naturaleza, no solamente por tecnología.
- Cada concepto vive en un único documento canónico.
- Las carpetas se crean cuando llega contenido real.
- Los documentos antiguos se migran gradualmente.
- Los planes históricos se conservan, pero no gobiernan la estructura actual.

## 3. Estructura objetivo

```text
The-Dev-Guide/
|-- README.md
|-- AGENTS.md
|-- CLAUDE.md
|-- PLAN-ACCION.md
|-- fundamentals/
|-- languages/
|   `-- javascript/
|-- technologies/
|   |-- react/
|   |-- redux/
|   |-- angular/
|   |-- nodejs/
|   `-- dotnet/
|-- tools/
|   |-- git/
|   `-- setup/
|-- _inbox/
|-- _archive/
|-- _templates/
`-- _session-log/
```

Esta es una estructura de referencia. No deben crearse carpetas vacías.

## 4. Mapa de clasificación

| Pregunta | Ubicación |
|---|---|
| ¿El concepto aplica sin importar el lenguaje? | `fundamentals/` |
| ¿Es una característica propia de un lenguaje? | `languages/<lenguaje>/` |
| ¿Es un framework, librería o runtime? | `technologies/<nombre>/` |
| ¿Es una herramienta o servicio de trabajo? | `tools/<nombre>/` |
| ¿Todavía no sabemos dónde va? | `_inbox/` |

Ejemplos acordados:

```text
fundamentals/testing.md
languages/javascript/arrays.md
technologies/react/componentes.md
technologies/redux/README.md
tools/git/pull-clone-fetch.md
```

## 5. Flujo para conceptos nuevos

1. Humberto envía un concepto, duda o explicación previa.
2. La IA busca si el tema ya existe.
3. Se decide el documento canónico y los conceptos relacionados.
4. Se explica el tema usando la plantilla.
5. Se añaden ejemplos, práctica y fuentes.
6. Se actualiza el índice correspondiente.
7. Se revisa el diff.
8. Humberto valida el contenido.
9. El estado cambia de `generated` a `verified` cuando corresponda.
10. Se hace un commit atómico si Humberto lo solicita.

## 6. Backlog

### Base del repositorio

- [x] Definir clasificación neutral.
- [x] Crear `AGENTS.md`.
- [x] Crear puente `CLAUDE.md`.
- [x] Unificar la plantilla documental.
- [x] Actualizar la portada.
- [ ] Revisar los documentos antiguos y agregarles front matter.
- [ ] Migrar `01-git/` a `tools/git/`.
- [ ] Migrar `02-setup/` a una ubicación definitiva.

### Primeros conceptos

- [ ] Crear fundamentos de testing.
- [x] Crear guía de Redux.
- [ ] Crear índice de JavaScript cuando llegue el primer concepto.
- [x] Crear índice de React cuando llegue el primer concepto.
- [x] Clasificar y documentar el temario inicial de React.
- [x] Separar gestión de estado y arquitectura como fundamentos.
- [x] Separar modelado de datos como tema de TypeScript.
- [x] Crear guías iniciales de React Router, SWR, Zustand y Jotai.
- [x] Crear guías iniciales de React Hook Form y Axios.

Las tareas de contenido se realizan cuando Humberto envíe el concepto o pida
trabajarlo. No se generan carpetas ni documentos de relleno.

## 7. Criterio de calidad

Un documento está listo para revisión cuando:

- explica el propósito antes de la API;
- distingue cuándo usar y cuándo no usar el concepto;
- contiene al menos un ejemplo útil;
- registra confusiones frecuentes;
- propone una forma de práctica;
- enlaza fuentes oficiales;
- no duplica otro documento;
- tiene front matter y fecha actualizados.

Un documento se marca `verified` únicamente cuando fue revisado o probado. Un
texto convincente no cuenta automáticamente como verificación.

## 8. Commits

Un commit representa una intención cerrada:

```text
docs: define reglas compartidas para agentes
docs: agrega fundamentos de testing
docs: agrega guia de redux
docs: migra documentacion de git
```

Antes de un commit:

1. Revisar `git status`.
2. Revisar el diff.
3. Confirmar que no hay secretos.
4. Verificar enlaces y ejemplos.
5. Incluir solamente archivos relacionados con la intención.

## 9. Próximo paso

Elegir uno de los documentos con estado `generated`, estudiarlo con ejemplos y
convertirlo en `verified`, o recibir el siguiente concepto de Humberto.
