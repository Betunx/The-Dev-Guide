---
title: TypeScript en React
status: generated
tags: [react, typescript, react-node, jsx-element]
related:
  - ../../languages/typescript/modelado-de-datos.md
sources:
  - https://react.dev/learn/typescript
updated: 2026-06-08
---

# TypeScript en React

## `ReactNode`, `ReactElement` y `JSX.Element`

| Tipo | Representa | Uso típico |
|---|---|---|
| `React.ReactNode` | cualquier contenido renderizable | `children` |
| `React.ReactElement` | un elemento React creado | retorno o prop que exige un elemento |
| `JSX.Element` | tipo global/histórico de una expresión JSX | código existente |

`ReactNode` es más amplio: puede incluir elementos, strings, números, arrays,
portals, `null`, `undefined` y booleanos renderizables.

```tsx
type CardProps = {
  title: string;
  children: React.ReactNode;
};
```

Si una API necesita exactamente un elemento para clonarlo o inspeccionarlo,
`ReactElement` comunica mejor esa restricción.

## Props

```tsx
type ButtonProps = {
  variant?: "primary" | "secondary";
  onClick: () => void;
  children: React.ReactNode;
};
```

Usa uniones de literales para variantes válidas y tipos explícitos para
callbacks.

## Eventos y refs

```tsx
function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
  console.log(event.currentTarget.value);
}

const inputRef = useRef<HTMLInputElement>(null);
```

## Estado

Permite inferencia cuando el valor inicial es suficiente:

```tsx
const [count, setCount] = useState(0);
```

Declara el genérico cuando hay ausencia o varios estados:

```tsx
const [user, setUser] = useState<User | null>(null);
```

Para reducers, usa una unión discriminada para las acciones.

## Confusión frecuente

TypeScript no valida props o respuestas HTTP durante ejecución. Los tipos se
eliminan al compilar; los datos externos necesitan validación runtime.

## Práctica

¿Qué tipo usarías para una prop `children` que admite texto, fragmentos y
elementos?

<details>
<summary>Ver respuesta</summary>

`React.ReactNode`.

</details>

