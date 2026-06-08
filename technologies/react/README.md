---
title: React
status: generated
tags: [react, frontend, components, index]
related:
  - ../../fundamentals/gestion-de-estado.md
  - ../react-router/README.md
sources:
  - https://react.dev/learn
  - https://react.dev/reference/react
updated: 2026-06-08
---

# React

> React es una librería para describir interfaces mediante componentes y
> actualizar la UI cuando cambian sus datos.

## Por qué existe

En una interfaz imperativa, el programa busca elementos y modifica el DOM paso
a paso. React propone declarar cómo debería verse la interfaz para un estado
determinado:

```tsx
function SaveButton({ isSaving }: { isSaving: boolean }) {
  return <button disabled={isSaving}>{isSaving ? "Guardando..." : "Guardar"}</button>;
}
```

Cuando los datos cambian, React vuelve a calcular la descripción de la UI y
aplica al DOM solamente los cambios necesarios.

## Qué aporta

- Componentes reutilizables y componibles.
- Flujo de datos principalmente descendente mediante props.
- Estado local y Hooks para comportamiento.
- Renderizado declarativo.
- Ecosistema para routing, formularios, estado y frameworks completos.

React no incluye oficialmente router, cliente HTTP ni store global. Esas son
decisiones separadas.

## Cuándo usarlo

- Interfaces interactivas con muchas piezas que cambian.
- Equipos que quieren composición y ecosistema amplio.
- Aplicaciones donde un framework basado en React aporta routing, datos o SSR.

Puede ser innecesario para una página estática pequeña sin interacción.

## Ruta de estudio

1. [Estado y comunicación](./estado-y-comunicacion.md)
2. [Renderizado y rendimiento](./renderizado-y-rendimiento.md)
3. [Effects, referencias y custom hooks](./efectos-referencias-y-custom-hooks.md)
4. [Patrones de componentes y portals](./patrones-de-componentes.md)
5. [Suspense y carga diferida](./suspense-y-lazy.md)
6. [TypeScript en React](./typescript-en-react.md)
7. [Estilos](./estilos.md)
8. [React 19 y React Compiler](./react-19-y-compiler.md)

## Preguntas frecuentes de entrevista

### ¿React es un framework?

React se presenta como librería de UI. Puede formar parte de un framework que
añada routing, renderizado de servidor y carga de datos.

### ¿Qué diferencia hay entre render y commit?

Render calcula qué debería mostrarse. Commit aplica al DOM las diferencias
necesarias. Un render no implica necesariamente un cambio real en el DOM.

### ¿Qué provoca un render?

El montaje inicial, una actualización de estado, un cambio de Context o el
render de un ancestro. Las props nuevas se observan cuando el padre renderiza.

### ¿Las props son inmutables?

El componente debe tratarlas como valores de solo lectura. Para cambiar la UI,
el dueño del dato actualiza estado y entrega props nuevas.

### ¿React vuelve a crear las funciones?

Sí, el cuerpo de un componente se ejecuta en cada render. Eso normalmente no es
un problema; solo se optimiza cuando existe una razón medida.

## Práctica

Explica React sin usar las palabras "rápido" ni "Virtual DOM".

<details>
<summary>Ver respuesta</summary>

React permite describir la interfaz como una función de props y estado,
organizarla en componentes y sincronizar el DOM cuando esos datos cambian.

</details>

