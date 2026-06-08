---
title: Gestión de estado en frontend
status: generated
tags: [state, frontend, react, server-state]
related:
  - ../technologies/react/estado-y-comunicacion.md
  - ../technologies/redux/README.md
  - ../technologies/swr/README.md
  - ../technologies/zustand/README.md
  - ../technologies/jotai/README.md
sources:
  - https://react.dev/learn/managing-state
  - https://reactrouter.com/explanation/state-management
  - https://redux.js.org/introduction/getting-started
updated: 2026-06-08
---

# Gestión de estado en frontend

> Antes de elegir una librería, identifica qué clase de estado estás
> administrando y quién debe ser su dueño.

## Idea principal

Estado es información que puede cambiar y que afecta el comportamiento o la
interfaz. El error común es guardar todo en una solución "global". La decisión
correcta suele ser mantener cada dato tan cerca como sea posible de quienes lo
usan.

`Single source of truth` no significa que toda la aplicación tenga un único
objeto global. Significa que cada dato tiene un dueño canónico y no se duplica
en lugares que puedan quedar desincronizados.

## Tipos de estado

| Tipo | Ejemplos | Primera opción |
|---|---|---|
| Local de UI | modal abierto, pestaña, input | `useState` |
| Compartido cercano | dos hermanos coordinados | elevar estado al padre |
| Compartido profundo | tema, sesión, configuración | Context |
| Complejo de una pantalla | wizard, editor, muchas transiciones | `useReducer` |
| URL | filtros, página, búsqueda | router y search params |
| Servidor | usuarios, productos, caché HTTP | SWR, RTK Query u otra librería de fetching |
| Global de cliente | carrito, preferencias, workflow transversal | Redux, Zustand o Jotai |
| Formulario | valores, errores, touched, dirty | React Hook Form o estado local |

## Escalera de decisión

1. Valor constante o derivable: no es estado.
2. Un componente: `useState`.
3. Varios componentes cercanos: elevarlo al ancestro común.
4. Árbol profundo estable: Context.
5. Transiciones complejas: `useReducer`.
6. Datos remotos: herramienta de server state.
7. Estado de cliente realmente transversal: store externo.

## Comparación rápida

| Solución | Modelo | Buena para | Costo principal |
|---|---|---|---|
| Context | valor por árbol de providers | dependencias globales estables | rerenders y providers grandes |
| Redux Toolkit | store, acciones, reducers | reglas complejas y trazabilidad | estructura adicional |
| Zustand | store con hook y selectores | estado global simple | menos convenciones de equipo |
| Jotai | átomos componibles | dependencias granulares | diseño de átomos |
| SWR | caché por clave | datos del servidor | no sustituye estado de UI |
| RTK Query | caché integrada con Redux | server state en apps Redux | acoplamiento al stack Redux |

## Confusiones frecuentes

### Guardar respuestas HTTP en Context

Context comparte un valor, pero no resuelve por sí solo caché, deduplicación,
revalidación, cancelación ni estados de petición.

### Duplicar props en estado

Si un valor puede calcularse desde props u otro estado durante el render, casi
siempre conviene derivarlo en lugar de sincronizar otra copia con un Effect.

### Elegir por popularidad

La herramienta se elige por el problema. Un modal no necesita Redux y una
caché de servidor compleja no debería construirse a mano con varios Context.

## Práctica

Clasifica estos datos: filtro de productos compartible por URL, token de sesión,
texto de un input y respuesta de `/api/products`.

<details>
<summary>Ver respuesta</summary>

- Filtro: URL/search params.
- Sesión: Context o store según su complejidad.
- Input: estado local o librería de formularios.
- Productos remotos: server state, por ejemplo SWR o RTK Query.

</details>
