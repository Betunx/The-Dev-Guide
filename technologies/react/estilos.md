---
title: Estilos en React
status: generated
tags: [react, css, scss, css-modules, styling]
related: []
sources:
  - https://react.dev/reference/react-dom/components/common
  - https://github.com/css-modules/css-modules
  - https://sass-lang.com/documentation/
updated: 2026-06-08
---

# Estilos en React

> React no impone un sistema de estilos. La elección depende del alcance,
> dinamismo, herramientas del proyecto y convenciones del equipo.

## CSS global

Simple y nativo. Conviene para resets, tokens y estilos base. El riesgo es la
colisión de nombres y el alcance global.

## CSS Modules

```tsx
import styles from "./Button.module.css";

<button className={styles.primary}>Guardar</button>
```

Genera nombres con alcance local. Es una buena opción por defecto para
componentes sin introducir una librería runtime.

## Sass/SCSS

Añade variables, mixins, nesting y otras herramientas de preprocesado. Puede
combinarse con Modules: `Button.module.scss`.

Evita nesting profundo, porque aumenta especificidad y acoplamiento al DOM.

## Variables CSS

```css
:root {
  --color-primary: #2563eb;
}
```

Son ideales para design tokens, temas y valores que cambian en runtime. Pueden
usarse desde CSS global, Modules o estilos inline.

## Objeto inline `style`

```tsx
<div style={{ width: progress + "%", opacity: disabled ? 0.5 : 1 }} />
```

Es útil para valores dinámicos calculados. No soporta directamente
pseudoclases ni media queries y puede mezclar demasiada presentación con
lógica.

## CSS-in-JS

Librerías externas permiten estilos dinámicos y encapsulación con distintos
costos de runtime, bundle y configuración. Evalúa si el proyecto realmente
necesita esa capacidad.

## Guía rápida

| Necesidad | Opción inicial |
|---|---|
| Base y tokens | CSS global + variables |
| Componente aislado | CSS Modules |
| Preprocesado existente | SCSS Modules |
| Valor calculado puntual | `style` |
| Sistema dinámico complejo | evaluar CSS-in-JS |

## Práctica

¿Usarías inline style para `:hover` y responsive?

<details>
<summary>Ver respuesta</summary>

No como primera opción. CSS, Modules o una solución de styling manejan mejor
pseudoclases y media queries.

</details>

