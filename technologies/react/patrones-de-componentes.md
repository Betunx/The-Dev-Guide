---
title: Patrones de componentes React
status: generated
tags: [react, composition, portals, hoc, components]
related:
  - estado-y-comunicacion.md
  - ../../fundamentals/arquitectura-frontend.md
sources:
  - https://react.dev/learn/passing-props-to-a-component
  - https://react.dev/learn/passing-data-deeply-with-context
  - https://react.dev/reference/react-dom/createPortal
updated: 2026-06-08
---

# Patrones de componentes React

## Composición

React favorece construir piezas grandes combinando componentes pequeños.
`children` y props que reciben JSX permiten personalizar estructura sin crear
dependencias globales.

```tsx
function Modal({ children }: { children: React.ReactNode }) {
  return <div className="modal">{children}</div>;
}
```

La composición suele ser preferible a Context cuando un ancestro ya sabe qué
contenido debe colocar y los intermediarios no necesitan conocer los datos.

## Container y presentational

- Container: coordina datos, estado y acciones.
- Presentational: recibe props y renderiza UI.

No es obligatorio separar cada componente en dos archivos. Úsalo cuando mejora
pruebas, reutilización o lectura.

## Higher-Order Components

Un HOC es una función que recibe un componente y devuelve otro:

```tsx
function withPermission<P>(Component: React.ComponentType<P>) {
  return function Protected(props: P) {
    return canAccess() ? <Component {...props} /> : null;
  };
}
```

Fue común para reutilizar comportamiento antes de Hooks. Sigue apareciendo en
librerías y código legado, pero custom hooks y composición suelen producir
árboles y tipos más sencillos.

Riesgos:

- colisiones de props;
- wrappers difíciles de seguir;
- pérdida de nombres útiles en DevTools;
- genéricos complejos en TypeScript.

## Portals

`createPortal` renderiza DOM en otro contenedor sin sacar al elemento del árbol
de React.

```tsx
return createPortal(<Dialog />, document.body);
```

Casos comunes:

- modales;
- tooltips;
- menús flotantes;
- overlays que deben escapar de `overflow` o stacking contexts.

Aunque el DOM esté en otro sitio, Context y propagación de eventos siguen el
árbol de React. Debes manejar foco, Escape, bloqueo de scroll y accesibilidad.

## Custom hook vs componente

- Custom hook: reutiliza lógica con estado o Effects.
- Componente: reutiliza estructura y UI.
- Función normal: reutiliza cálculo puro.
- HOC: adapta un componente completo.

## Práctica

Necesitas reutilizar la suscripción al estado online en tres UIs distintas.
¿Componente, HOC o custom hook?

<details>
<summary>Ver respuesta</summary>

Un custom hook expresa mejor la reutilización de lógica. Cada componente
conserva control sobre su presentación.

</details>

