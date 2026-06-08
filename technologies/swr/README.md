---
title: SWR
status: generated
tags: [swr, server-state, cache, data-fetching]
related:
  - ../../fundamentals/gestion-de-estado.md
  - ../redux/README.md
sources:
  - https://swr.vercel.app/
  - https://swr.vercel.app/docs/revalidation
  - https://swr.vercel.app/docs/mutation
updated: 2026-06-08
---

# SWR

> SWR administra datos remotos con caché y revalidación mediante un Hook.

## Significado

El término correcto es **stale-while-revalidate**: mostrar temporalmente datos
en caché y, al mismo tiempo, solicitar una versión fresca.

```tsx
const { data, error, isLoading, isValidating } = useSWR(
  "/api/user",
  fetcher,
);
```

La `key` identifica el recurso. El `fetcher` sabe cómo obtenerlo.

## Qué resuelve

- caché;
- deduplicación de peticiones;
- revalidación al recuperar foco o conexión;
- revalidación periódica opcional;
- estados de carga y error;
- mutaciones y actualizaciones optimistas.

`isLoading` indica que todavía no hay datos; `isValidating` puede ser verdadero
durante cualquier revalidación, incluso cuando ya existe caché visible.

## Cuándo usarlo

- Aplicación React que necesita server state sin Redux.
- Datos que deben refrescarse al volver a la pestaña.
- APIs donde una clave representa naturalmente un recurso.

No es la primera opción para estado puramente local como un modal o un draft de
formulario.

## SWR vs Redux/Zustand/Jotai

SWR se centra en sincronizar una caché con el servidor. Los otros stores se
centran principalmente en estado de cliente. Pueden coexistir.

## Práctica

¿Por qué SWR puede mostrar datos y `isValidating: true` al mismo tiempo?

<details>
<summary>Ver respuesta</summary>

Porque muestra la copia en caché mientras consulta una versión más reciente.

</details>

