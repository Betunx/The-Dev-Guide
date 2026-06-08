---
title: React Router
status: generated
tags: [react-router, routing, url, navigation]
related:
  - ../react/README.md
  - ../../fundamentals/gestion-de-estado.md
sources:
  - https://reactrouter.com/start/data/routing
  - https://reactrouter.com/api/hooks/useParams
  - https://reactrouter.com/api/hooks/useSearchParams
  - https://reactrouter.com/api/utils/redirect
updated: 2026-06-08
---

# React Router

> React Router relaciona segmentos de URL con componentes, layouts, datos y
> acciones. No forma parte del núcleo de React.

## Enrutamiento básico

En aplicaciones web se instala normalmente mediante `react-router-dom`. La
documentación moderna también muestra imports desde `react-router` según el
modo de uso.

```tsx
const router = createBrowserRouter([
  {
    path: "/",
    Component: RootLayout,
    children: [
      { index: true, Component: HomePage },
      { path: "users/:userId", Component: UserPage },
    ],
  },
]);
```

## Rutas hijas

Las rutas anidadas se declaran con `children`. El padre debe renderizar
`<Outlet />` para indicar dónde aparece el hijo.

```tsx
function DashboardLayout() {
  return (
    <>
      <DashboardNav />
      <Outlet />
    </>
  );
}
```

Las rutas `index` son el hijo por defecto para la URL del padre.

## Parámetros de ruta

Para `/users/:userId`:

```tsx
const { userId } = useParams();
```

Los hijos heredan los parámetros dinámicos de sus rutas padre.

## Query params

Para `/products?page=2&sort=price`:

```tsx
const [searchParams, setSearchParams] = useSearchParams();
const page = Number(searchParams.get("page") ?? "1");
```

Los filtros compartibles, búsqueda, orden y paginación suelen pertenecer a la
URL en vez de duplicarse en estado global.

## Protección de rutas

React Router no usa el concepto oficial de `guard` como Angular. Dos patrones
comunes:

### Redirección en un loader

```tsx
async function dashboardLoader({ request }: LoaderArgs) {
  const user = await getCurrentUser(request);
  if (!user) throw redirect("/login");
  return user;
}
```

Evita renderizar primero la pantalla protegida.

### Layout protegido

```tsx
function ProtectedLayout() {
  const user = useAuth();
  return user ? <Outlet /> : <Navigate to="/login" replace />;
}
```

Es útil en modo declarativo o cuando la sesión ya está disponible en cliente.
La autorización real también debe validarse en el servidor; ocultar una ruta
no protege una API.

## Loaders

Los loaders cargan datos antes del componente de la ruta en los modos que los
soportan. Reciben `request`, `params` y señal de cancelación, y ayudan a evitar
fetching encadenado en Effects.

## Práctica

¿Dónde guardarías `?category=books&page=3`: Redux o URL?

<details>
<summary>Ver respuesta</summary>

En la URL. Es navegación compartible, recargable y compatible con historial.

</details>

