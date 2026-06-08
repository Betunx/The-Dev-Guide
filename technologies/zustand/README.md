---
title: Zustand
status: generated
tags: [zustand, state, store, react]
related:
  - ../../fundamentals/gestion-de-estado.md
  - ../redux/README.md
  - ../jotai/README.md
sources:
  - https://zustand.docs.pmnd.rs/getting-started/introduction
  - https://github.com/pmndrs/zustand
updated: 2026-06-08
---

# Zustand

> Zustand ofrece un store externo pequeño con una API basada en hooks y
> selectores.

## Ejemplo

```ts
type CounterStore = {
  count: number;
  increment: () => void;
};

export const useCounterStore = create<CounterStore>((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}));
```

```tsx
const count = useCounterStore((state) => state.count);
```

El selector hace que el componente se suscriba a la porción necesaria.

## Ventajas

- poco boilerplate;
- no requiere Provider para el caso común;
- acciones y estado pueden vivir juntos;
- acceso fuera de React mediante la API del store;
- middleware para persistencia y DevTools.

## Riesgos

- Un store gigante puede convertirse en variable global desordenada.
- Seleccionar objetos nuevos en cada llamada puede provocar renders.
- La libertad de estructura requiere convenciones del equipo.
- Persistir no significa que todos los datos deban guardarse.

## Cuándo usarlo

Estado transversal de cliente que supera Context pero no necesita el flujo y
convenciones de Redux Toolkit.

## Práctica

¿Por qué seleccionar `state.count` es mejor que consumir todo el store?

<details>
<summary>Ver respuesta</summary>

Reduce el alcance de la suscripción: el componente solo necesita reaccionar a
la parte utilizada.

</details>

