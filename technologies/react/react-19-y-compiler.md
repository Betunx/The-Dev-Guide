---
title: React 19 y React Compiler
status: generated
tags: [react, react-19, react-compiler, actions]
related:
  - renderizado-y-rendimiento.md
sources:
  - https://react.dev/blog/2024/12/05/react-19
  - https://react.dev/blog/2024/04/25/react-19-upgrade-guide
  - https://react.dev/blog/2025/10/01/react-19-2
  - https://react.dev/blog/2025/10/07/react-compiler-1
updated: 2026-06-08
---

# React 19 y React Compiler

> React 19 y React Compiler están relacionados, pero no son lo mismo. React es
> la librería; Compiler es una herramienta de build que optimiza código.

## Línea actual

React 19 se publicó el 5 de diciembre de 2024. React 19.2 se publicó el 1 de
octubre de 2025 y es la versión menor más reciente documentada oficialmente al
revisar esta guía el 8 de junio de 2026.

## Cambios principales de React 19

### Actions

React formalizó funciones async ejecutadas dentro de transiciones para manejar
pending, errores y actualizaciones optimistas.

APIs relacionadas:

- `useActionState`;
- `useOptimistic`;
- acciones en `<form>`;
- `useFormStatus`;
- `use`.

### `ref` como prop

Los componentes de función pueden recibir `ref` como prop, reduciendo la
necesidad de `forwardRef` en código nuevo.

### Recursos y metadatos

React puede manejar elementos como `title`, `meta`, `link`, `style` y scripts
con nuevas capacidades de posicionamiento, prioridad y carga.

### Mejoras de Suspense y errores

React 19 ajustó cuándo se confirma un fallback y cómo se reportan errores de
render. Revisa integraciones de observabilidad durante una migración.

### TypeScript y APIs retiradas

La guía de actualización incluye cambios de tipos y eliminación de APIs
deprecadas. Para una app antigua, la recomendación oficial fue pasar primero
por React 18.3 para recibir advertencias.

## React 19.2

Añadió, entre otros:

- `<Activity />`;
- `useEffectEvent`;
- `cacheSignal`;
- tracks de rendimiento para Chrome DevTools;
- mejoras de SSR y Suspense.

No mezcles automáticamente una característica de 19.2 con la versión 19.0.

## React Compiler

React Compiler 1.0 se publicó el 7 de octubre de 2025. Es una herramienta de
build que aplica memoización automática a componentes y Hooks.

Consecuencias:

- reduce la necesidad de `memo`, `useMemo` y `useCallback` manuales;
- depende de que el código siga las Rules of React;
- no corrige Effects incorrectos ni renders impuros;
- debe adoptarse y medirse como parte del toolchain.

La existencia del Compiler no convierte toda memoización manual en error.
Primero entiende el comportamiento y después elimina optimizaciones redundantes
con medición.

## Pregunta de entrevista

### ¿React Compiler reemplaza `useMemo`?

Automatiza muchas optimizaciones equivalentes, pero `useMemo` sigue existiendo.
El Compiler no sustituye el diseño de estado, la pureza ni el profiling.

## Práctica

¿React Compiler es una característica exclusiva del runtime de React 19?

<details>
<summary>Ver respuesta</summary>

No. Es una herramienta separada de compilación. Su versión estable 1.0 se
publicó después de React 19.

</details>
