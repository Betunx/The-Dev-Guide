---
title: Estado y comunicación en React
status: generated
tags: [react, state, context, use-state, use-reducer, composition]
related:
  - ../../fundamentals/gestion-de-estado.md
  - ../redux/README.md
sources:
  - https://react.dev/learn/managing-state
  - https://react.dev/learn/sharing-state-between-components
  - https://react.dev/learn/passing-data-deeply-with-context
  - https://react.dev/learn/queueing-a-series-of-state-updates
updated: 2026-06-08
---

# Estado y comunicación en React

> El mejor estado suele ser el mínimo necesario, con un dueño claro y ubicado
> cerca de quienes lo utilizan.

## `useState`

Se usa para información local que cambia y afecta el render.

```tsx
const [count, setCount] = useState(0);
```

No guardes como estado un valor que puede derivarse durante el render:

```tsx
const fullName = `${firstName} ${lastName}`;
```

## Actualización funcional y batching

React agrupa actualizaciones para evitar renders intermedios innecesarios. El
valor leído por un handler pertenece al snapshot de ese render.

```tsx
setCount((current) => current + 1);
setCount((current) => current + 1);
```

Usa la forma funcional cuando el siguiente valor depende del anterior,
especialmente con varias actualizaciones en la misma tarea.

## `useReducer`

Conviene cuando existen varias transiciones relacionadas o la lógica de
actualización ya no es clara con setters dispersos.

```tsx
type Action =
  | { type: "added"; payload: { id: string; text: string } }
  | { type: "removed"; payload: { id: string } };

function reducer(state: Todo[], action: Action): Todo[] {
  switch (action.type) {
    case "added":
      return [...state, action.payload];
    case "removed":
      return state.filter((todo) => todo.id !== action.payload.id);
  }
}
```

La acción describe qué ocurrió. `payload` transporta los datos necesarios. El
reducer calcula el siguiente estado y debe mantenerse puro.

## Padre a hijo

Las props son la opción directa:

```tsx
<UserCard user={user} onSelect={handleSelect} />
```

El hijo informa al padre mediante callbacks recibidos como props.

## Componentes hermanos

Eleva el estado a su ancestro común:

```text
Parent owns state
  -> Child A receives value
  -> Child B receives value and callback
```

En React no suele ser necesario crear un servicio con observables para
comunicar hermanos. RxJS puede ser válido al integrar streams complejos, pero
no es el mecanismo base de comunicación de React.

## Prop drilling, composición y Context

Prop drilling significa atravesar componentes que no usan el dato. Antes de
Context, prueba composición:

```tsx
function Page() {
  return <Layout sidebar={<UserMenu user={user} />} />;
}
```

La composición permite que el componente superior prepare JSX y evita que
`Layout` conozca datos que no utiliza.

Context conviene cuando muchos descendientes necesitan una dependencia como
tema, sesión, idioma o configuración.

```tsx
const AuthContext = createContext<Auth | null>(null);
```

Context no es automáticamente un store global: su alcance depende del
`Provider`. Cuando cambia su valor, los consumidores pueden renderizar de
nuevo. Separa contexts por responsabilidad y estabiliza su API cuando exista
un problema real.

## Estado por página

Mantén el estado dentro del componente de página o layout cuando solo esa rama
lo utiliza. Subir todo a la raíz aumenta acoplamiento y rerenders.

## Orden recomendado

1. Props.
2. Composición.
3. Elevar estado.
4. Context para dependencias profundas.
5. Store externo cuando la complejidad lo justifique.

## Práctica

Dos campos hermanos deben permanecer sincronizados. ¿Context o estado en el
padre?

<details>
<summary>Ver respuesta</summary>

Estado en el padre común. Context sería una dependencia adicional para un dato
que ya puede viajar directamente mediante props.

</details>

