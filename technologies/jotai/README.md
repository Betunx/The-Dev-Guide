---
title: Jotai
status: generated
tags: [jotai, atoms, state, react]
related:
  - ../../fundamentals/gestion-de-estado.md
  - ../zustand/README.md
sources:
  - https://jotai.org/
  - https://jotai.org/docs/core/atom
updated: 2026-06-08
---

# Jotai

> Jotai administra estado React como átomos pequeños y componibles.

## Átomo

Un átomo define una unidad de estado:

```ts
const countAtom = atom(0);
```

Un componente puede leerla y escribirla:

```tsx
const [count, setCount] = useAtom(countAtom);
```

Se siente parecido a `useState`, pero el valor vive en un store y puede ser
usado por componentes distantes dentro del alcance correspondiente.

## Átomos derivados

```ts
const doubleCountAtom = atom((get) => get(countAtom) * 2);
```

Jotai rastrea dependencias entre átomos y actualiza consumidores de manera
granular.

## Cuándo usarlo

- Estado global compuesto por piezas independientes.
- Datos derivados entre unidades pequeñas.
- Se busca una API cercana al modelo de Hooks.
- El grafo de dependencias es más natural que un store monolítico.

## Jotai vs Zustand

- Jotai: modelo bottom-up de átomos y derivaciones.
- Zustand: store explícito con estado, acciones y selectores.

Ninguno es universalmente mejor. Elige el modelo que haga más claras las reglas
del dominio.

## Confusión frecuente

Jotai no hace que cada `useState` sea global. Debes crear y compartir un átomo.
Cada llamada a un custom hook normal sigue teniendo estado independiente salvo
que use una fuente compartida.

## Práctica

¿Qué usarías para calcular un total desde `priceAtom` y `quantityAtom`?

<details>
<summary>Ver respuesta</summary>

Un átomo derivado que lea ambos y retorne `price * quantity`.

</details>
