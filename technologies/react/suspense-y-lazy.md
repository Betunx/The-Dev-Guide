---
title: Suspense y lazy loading
status: generated
tags: [react, suspense, lazy, code-splitting]
related:
  - renderizado-y-rendimiento.md
  - ../react-router/README.md
sources:
  - https://react.dev/reference/react/Suspense
  - https://react.dev/reference/react/lazy
updated: 2026-06-08
---

# Suspense y lazy loading

> `lazy` difiere la carga del código de un componente y `Suspense` define qué
> mostrar mientras una parte del árbol todavía no está lista.

## `lazy`

```tsx
const ReportsPage = lazy(() => import("./ReportsPage"));
```

Debe declararse fuera del componente para no crear un tipo distinto en cada
render. Normalmente el módulo cargado expone el componente como `default`.

## `Suspense`

```tsx
<Suspense fallback={<PageSkeleton />}>
  <ReportsPage />
</Suspense>
```

La boundary muestra `fallback` cuando un descendiente suspende. La ubicación
de las boundaries define qué parte de la interfaz se reemplaza y con qué
granularidad.

## Qué afecta

- Reduce el JavaScript inicial cuando se divide código.
- Puede mostrar fallback durante la primera carga.
- Una boundary demasiado alta oculta demasiada UI.
- Muchas boundaries pequeñas pueden producir una experiencia fragmentada.
- Frameworks compatibles pueden integrar streaming e hidratación selectiva.

Suspense no convierte automáticamente cualquier `fetch` dentro de un Effect en
una fuente compatible. Para datos, usa una integración o framework que soporte
Suspense explícitamente.

## Con React Router

Las rutas son un límite natural para dividir bundles. React Router también
ofrece rutas lazy y mecanismos de carga de datos según el modo utilizado.

## Práctica

¿Conviene colocar una sola boundary alrededor de toda la aplicación?

<details>
<summary>Ver respuesta</summary>

Puede servir como último fallback, pero boundaries cercanas a secciones
independientes suelen conservar más UI visible y dar mejor retroalimentación.

</details>

