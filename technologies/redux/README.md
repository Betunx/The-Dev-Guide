---
title: Redux Toolkit y RTK Query
status: generated
tags: [redux, redux-toolkit, rtk-query, state]
related:
  - ../../fundamentals/gestion-de-estado.md
  - ../react/estado-y-comunicacion.md
sources:
  - https://redux.js.org/introduction/getting-started
  - https://redux-toolkit.js.org/introduction/getting-started
  - https://redux-toolkit.js.org/rtk-query/overview
updated: 2026-06-08
---

# Redux Toolkit y RTK Query

> Redux administra estado global predecible. Redux Toolkit es la forma oficial
> recomendada de escribir Redux; RTK Query administra fetching y caché.

## ¿Pertenece a React?

No. Redux es una librería JavaScript independiente de la UI. `react-redux`
ofrece los bindings para usar un store Redux desde componentes React.

## Modelo mental

```text
UI -> dispatch(action) -> reducer -> nuevo store -> UI suscrita
```

- Store: árbol de estado.
- Action: objeto que describe qué ocurrió.
- Payload: datos de la acción.
- Reducer: función pura que calcula el siguiente estado.
- Selector: función que lee o deriva datos.

## Redux Toolkit

```ts
const cartSlice = createSlice({
  name: "cart",
  initialState: { items: [] as Item[] },
  reducers: {
    itemAdded(state, action: PayloadAction<Item>) {
      state.items.push(action.payload);
    },
  },
});
```

`createSlice` genera reducer y action creators. La sintaxis parece mutar, pero
Immer produce actualizaciones inmutables.

```ts
const store = configureStore({
  reducer: {
    cart: cartSlice.reducer,
  },
});
```

En React se usa `Provider`, `useSelector` y `useDispatch`, preferiblemente con
hooks tipados del proyecto.

## Cuándo usar Redux

- Muchas áreas modifican el mismo estado.
- Existen reglas y transiciones complejas.
- Se necesita trazabilidad con DevTools.
- El equipo valora convenciones estrictas.
- Hay estado de cliente transversal con vida larga.

No lo uses automáticamente para cada input, modal o respuesta HTTP.

## RTK Query

El nombre correcto es **RTK Query**, no "Redux Query". Está incluido en Redux
Toolkit y resuelve server state:

- fetching;
- caché y deduplicación;
- queries y mutations;
- invalidación por tags;
- polling y refetch;
- estados `isLoading`, `isFetching` y error;
- hooks React generados opcionalmente.

```ts
export const api = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
  tagTypes: ["User"],
  endpoints: (build) => ({
    getUser: build.query<User, string>({
      query: (id) => `/users/${id}`,
      providesTags: (_result, _error, id) => [{ type: "User", id }],
    }),
  }),
});
```

## Redux Toolkit vs RTK Query

- Slice normal: estado de cliente y reglas propias.
- RTK Query: copia sincronizada de datos del servidor.

Evita copiar manualmente la respuesta de RTK Query a otro slice sin una razón
clara; tendrías dos fuentes de verdad.

## Práctica

¿Un carrito local y una lista remota de productos van en la misma solución?

<details>
<summary>Ver respuesta</summary>

Pueden coexistir en Redux: slice para carrito y RTK Query para productos. Son
problemas distintos aunque compartan store.

</details>

