# AGENTS.md - The Dev Guide

Instrucciones para Claude Code, Codex, ChatGPT y cualquier IA que trabaje en
este repositorio.

## Propósito

The Dev Guide es la memoria técnica personal de Humberto. Debe servir para:

- aprender un concepto;
- recordarlo rápidamente;
- saber cuándo y cómo aplicarlo;
- practicarlo con ejemplos y ejercicios;
- registrar errores reales y sus soluciones.

No copiar documentación oficial. Explicar con palabras propias y enlazar las
fuentes utilizadas.

## Fuente de verdad

Este archivo contiene las reglas compartidas por todas las IAs.

Orden de lectura antes de editar:

1. `AGENTS.md`
2. `README.md`
3. `PLAN-ACCION.md`
4. El índice y los documentos del área que se modificará

`CLAUDE.md` existe solamente como puente para herramientas que buscan ese
nombre. Las reglas no se duplican allí.

## Clasificación

- `fundamentals/`: conceptos independientes de un lenguaje o framework, como
  testing, HTTP, OOP, SOLID, arquitectura y estructuras de datos.
- `languages/`: características propias de un lenguaje, como JavaScript,
  TypeScript, C# o SQL.
- `technologies/`: frameworks, librerías y runtimes, como React, Redux,
  Angular, Node.js y .NET.
- `tools/`: herramientas y servicios de trabajo, como Git, GitHub, Prettier,
  Docker, Vercel y la terminal.
- `_inbox/`: notas crudas o contenido cuya ubicación aún no está clara.
- `_archive/`: contenido deprecado que se conserva como referencia.

Ejemplos:

- testing general: `fundamentals/testing.md`
- métodos de arrays de JavaScript: `languages/javascript/arrays.md`
- componentes de React: `technologies/react/componentes.md`
- Redux: `technologies/redux/README.md`
- comandos de Git: `tools/git/`

Las carpetas históricas `01-git/` y `02-setup/` se conservan hasta que su
contenido se migre en una tarea dedicada. No mover archivos solo por estética.

## Regla de ubicación

Antes de crear un documento:

1. Buscar si el concepto ya existe.
2. Elegir un único archivo canónico.
3. En otros documentos, enlazar el archivo canónico en vez de copiarlo.
4. Si la ubicación no es clara, usar `_inbox/`.
5. No crear carpetas vacías.

Los nombres de archivos y carpetas deben estar en minúsculas y usar guiones:
`manejo-de-errores.md`.

## Formato de cada tema

Usar `_templates/plantilla-doc.md` como base. Cada tema debe incluir, cuando
aplique:

- qué es;
- por qué existe;
- cuándo usarlo y cuándo no;
- cómo funciona;
- ejemplo mínimo;
- formas comunes de aplicarlo;
- errores o confusiones frecuentes;
- ejercicio o preguntas de repaso;
- conceptos relacionados;
- fuentes oficiales.

No agregar secciones vacías solo para cumplir la plantilla.

## Front matter

Cada documento de contenido debe comenzar con:

```yaml
---
title: React Props
status: draft
tags: [react, props, jsx]
related:
  - technologies/react/jsx.md
sources:
  - https://react.dev/learn/passing-props-to-a-component
updated: 2026-06-08
---
```

Las rutas de `related` se escriben desde la ubicación del documento actual, no
desde la raíz del repositorio.

Valores válidos de `status`:

- `verified`: revisado o probado.
- `generated`: generado con IA y pendiente de validación.
- `draft`: borrador incompleto.
- `deprecated`: conservado como referencia, pero ya no recomendado.

Un contenido nuevo explicado por IA comienza como `generated`, salvo que haya
sido verificado durante la misma tarea. `updated` usa `YYYY-MM-DD`.

## Reglas para explicar conceptos

- Empezar con el modelo mental y el propósito, no con una lista de APIs.
- Diferenciar concepto, herramienta e implementación.
- Preferir ejemplos pequeños que puedan ejecutarse o razonarse.
- Explicar los tradeoffs: cuándo ayuda, cuándo sobra y qué alternativas hay.
- Relacionar el tema con conocimientos existentes mediante `related`.
- Separar datos estables de información dependiente de versiones.
- Para información cambiante, consultar primero documentación oficial y anotar
  la versión o fecha relevante.
- No inventar experiencia personal del usuario ni afirmar que algo fue probado
  si no se ejecutó.

## Edición y flujo de trabajo

- Respetar notas y cambios existentes del usuario.
- Mantener cada tarea enfocada en una intención.
- Actualizar el índice del área cuando se agrega o mueve un tema.
- Revisar enlaces relativos, formato y ejemplos antes de cerrar.
- Mostrar o resumir el diff para que Humberto pueda revisarlo.
- No hacer commits ni push salvo que Humberto lo pida expresamente.
- Si se solicita commit, usar un mensaje atómico, por ejemplo:
  `docs: agrega fundamentos de testing`.

## Seguridad

- Nunca guardar claves, tokens, `.env` reales ni datos personales sensibles.
- Usar placeholders como `API_KEY=tu_clave_aqui`.
- Los archivos con secretos deben estar ignorados por Git.
- No incluir información privada de trabajos, salarios o conversaciones.
