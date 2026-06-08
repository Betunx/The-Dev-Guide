# The Dev Guide

> Memoria técnica personal para aprender, practicar y consultar conceptos de
> desarrollo sin depender de recordar todo de memoria.

**Última actualización:** 2026-06-08

## Propósito

Este repositorio reúne explicaciones con palabras propias, ejemplos pequeños,
ejercicios, errores frecuentes y fuentes oficiales.

No busca copiar documentación ni convertirse en un curso gigante. Cada tema
debe ayudar a responder:

- ¿Qué es?
- ¿Por qué existe?
- ¿Cuándo conviene usarlo?
- ¿Cómo funciona?
- ¿Cómo puedo practicarlo?

## Organización

La guía se clasifica por la naturaleza del conocimiento:

| Carpeta | Contenido | Ejemplos |
|---|---|---|
| `fundamentals/` | Conceptos independientes de una tecnología | testing, HTTP, SOLID |
| `languages/` | Características propias de lenguajes | JavaScript, TypeScript, C# |
| `technologies/` | Frameworks, librerías y runtimes | React, Redux, Angular, Node.js, .NET |
| `tools/` | Herramientas y servicios de trabajo | Git, Docker, Prettier, Vercel |
| `_inbox/` | Notas crudas o pendientes de clasificar | ideas de una sesión |
| `_archive/` | Contenido deprecado conservado como referencia | formas antiguas |

Las carpetas nacen cuando existe un tema real. No se crean directorios vacíos
solo para representar el plan futuro.

## Contenido actual

### Fundamentos

- [Gestión de estado en frontend](./fundamentals/gestion-de-estado.md)
- [Arquitectura frontend](./fundamentals/arquitectura-frontend.md)

### Lenguajes

- [TypeScript](./languages/typescript/README.md)

### Tecnologías

- [Índice de tecnologías](./technologies/README.md)
- [React](./technologies/react/README.md)
- [React Router](./technologies/react-router/README.md)
- [Redux Toolkit y RTK Query](./technologies/redux/README.md)
- [SWR](./technologies/swr/README.md)
- [Zustand](./technologies/zustand/README.md)
- [Jotai](./technologies/jotai/README.md)
- [React Hook Form](./technologies/react-hook-form/README.md)
- [Axios](./technologies/axios/README.md)

### Git y GitHub

- [Pull, clone y fetch](./01-git/pull-clone-fetch.md)
- [Autenticación con PAT y GitHub CLI](./01-git/auth-pat-y-gh-cli.md)

### Preparación de proyectos

- [Instalar dependencias en un proyecto Node](./02-setup/instalar-dependencias-node.md)

`01-git/` y `02-setup/` son rutas históricas. Se migrarán gradualmente a la
nueva clasificación cuando se trabaje específicamente en esos documentos.

## Cómo agregar un concepto

1. Buscar si ya existe un documento canónico.
2. Clasificarlo como fundamento, lenguaje, tecnología o herramienta.
3. Usar [`_templates/plantilla-doc.md`](./_templates/plantilla-doc.md).
4. Explicarlo con ejemplos y fuentes oficiales.
5. Enlazar conceptos relacionados sin duplicar contenido.
6. Actualizar el índice del área.
7. Revisar el cambio antes de hacer commit.

Los conceptos generados con ayuda de IA comienzan con `status: generated`.
Después de estudiarlos, probarlos o revisarlos, pueden cambiar a
`status: verified`.

## Trabajo con IA

Las reglas compartidas para Claude Code, Codex, ChatGPT y otras herramientas
están en [`AGENTS.md`](./AGENTS.md).

El flujo esperado es:

```text
concepto enviado
  -> buscar contenido existente
  -> elegir ubicación
  -> explicar y relacionar
  -> agregar al archivo canónico
  -> revisar diff
  -> validar
```

Una conversación puede ser amplia. El documento final debe quedar ordenado,
sin repeticiones y en la ubicación que le corresponde.

## Planeación

- [Plan de acción actual](./PLAN-ACCION.md)
- [Plan original conservado como contexto](./the-dev-guide-plan.md)

## Convenciones

- Un concepto tiene un solo documento canónico.
- Archivos y carpetas usan minúsculas y guiones.
- Fechas en formato `YYYY-MM-DD`.
- Los bloques de código indican su lenguaje.
- Las fuentes oficiales tienen prioridad.
- Los commits se hacen por intención, no por cantidad de archivos.
