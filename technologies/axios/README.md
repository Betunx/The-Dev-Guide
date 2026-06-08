---
title: Axios
status: generated
tags: [axios, http, api, interceptors, cancellation]
related:
  - ../swr/README.md
  - ../redux/README.md
sources:
  - https://axios-http.com/docs/instance
  - https://axios-http.com/docs/interceptors
  - https://axios-http.com/docs/cancellation
updated: 2026-06-08
---

# Axios

> Axios es un cliente HTTP. Facilita configurar instancias, transformar
> peticiones y respuestas, interceptar errores y cancelar solicitudes.

## Instancia para una API

```ts
export const api = axios.create({
  baseURL: "/api",
  timeout: 10_000,
  headers: {
    "Content-Type": "application/json",
  },
});
```

Una instancia centraliza configuración. Los módulos de cada feature pueden
exponer funciones con intención de dominio:

```ts
export async function getUser(id: string) {
  const response = await api.get<UserDto>(`/users/${id}`);
  return response.data;
}
```

El genérico describe el tipo esperado, pero Axios no valida que el servidor
realmente envíe esa forma.

## Interceptors

```ts
api.interceptors.request.use((config) => {
  const token = getToken();
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});
```

Casos habituales:

- agregar autenticación;
- normalizar errores;
- telemetría;
- renovación coordinada de token.

No registres interceptors durante cada render. Se acumularían y ejecutarían
varias veces. Si una integración los registra temporalmente, guarda el id y usa
`eject`.

Evita lógica de navegación o UI demasiado acoplada dentro de un interceptor.

## Cancelación

El nombre correcto en la lista probablemente era "cancelar/interrumpir
peticiones". Axios soporta `AbortController`:

```ts
const controller = new AbortController();

api.get("/users", {
  signal: controller.signal,
});

controller.abort();
```

La cancelación evita trabajo obsoleto cuando cambia una búsqueda, se desmonta
una pantalla o una nueva petición sustituye a otra. También configura timeout;
son protecciones complementarias.

## Axios vs fetch

`fetch` es estándar del navegador. Axios añade una API consistente para
instancias, interceptors, transformación y manejo de configuración. Elige por
necesidades del proyecto, no porque React requiera Axios.

## Con SWR o RTK Query

Axios obtiene datos. SWR y RTK Query administran caché y sincronización. Axios
puede funcionar como fetcher o base query personalizada, pero no reemplaza esas
responsabilidades.

## Práctica

¿Dónde registrarías un interceptor compartido: dentro de cada componente o en
la configuración de la instancia?

<details>
<summary>Ver respuesta</summary>

En la configuración de la instancia o en un ciclo de vida controlado. Dentro de
renders se registrarían handlers repetidos.

</details>

