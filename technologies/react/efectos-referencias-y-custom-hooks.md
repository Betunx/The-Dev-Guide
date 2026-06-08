---
title: Effects, referencias y custom hooks
status: generated
tags: [react, use-effect, use-ref, custom-hooks, async]
related:
  - renderizado-y-rendimiento.md
  - ../axios/README.md
sources:
  - https://react.dev/reference/react/useEffect
  - https://react.dev/reference/react/useRef
  - https://react.dev/learn/reusing-logic-with-custom-hooks
updated: 2026-06-08
---

# Effects, referencias y custom hooks

> `useEffect` sincroniza React con sistemas externos. No es el lugar genérico
> para ejecutar cualquier lógica después del render.

## Cuándo usar `useEffect`

- Suscribirse a eventos externos.
- Conectar y desconectar sockets.
- Controlar una API imperativa del navegador o una librería.
- Sincronizar una integración que React no administra.

Si solo calculas un valor desde props o estado, hazlo durante el render. Si
respondes a un click, hazlo en el handler.

## Dependencias

El arreglo contiene todos los valores reactivos usados por el setup:

```tsx
useEffect(() => {
  const connection = connect(serverUrl, roomId);
  return () => connection.disconnect();
}, [serverUrl, roomId]);
```

Valores reactivos incluyen props, estado y variables o funciones declaradas en
el componente. No se eligen por preferencia. Si una dependencia causa
ejecuciones excesivas, cambia la estructura del código en lugar de mentir al
linter.

| Segundo argumento | Comportamiento |
|---|---|
| omitido | después de cada commit |
| `[]` | montaje; en desarrollo Strict Mode prueba setup/cleanup extra |
| `[a, b]` | montaje y cambios de `a` o `b` según `Object.is` |

## Código async

La función principal del Effect no debe ser `async`, porque React espera que
retorne `undefined` o cleanup, no una Promise.

```tsx
useEffect(() => {
  const controller = new AbortController();

  async function load() {
    const response = await fetch(`/api/users/${id}`, {
      signal: controller.signal,
    });
    setUser(await response.json());
  }

  void load();
  return () => controller.abort();
}, [id]);
```

Para datos remotos complejos, prefiere loaders del framework o una librería de
server state que resuelva caché y carreras.

## Cleanup

El cleanup debe deshacer el setup:

- remover listeners;
- cancelar timers;
- cerrar conexiones;
- abortar peticiones;
- liberar recursos imperativos.

Strict Mode ayuda a revelar cleanups incompletos.

## `useRef`

`useRef` mantiene referencias DOM o datos mutables que no forman parte del
render. Cambiar `ref.current` no actualiza la pantalla.

## Custom hooks

Un custom hook encapsula lógica con Hooks:

```tsx
function useOnlineStatus() {
  // estado, suscripción y cleanup
}
```

Reglas:

- nombre con prefijo `use`;
- solo se llama en el nivel superior;
- comparte lógica, no una misma instancia de estado;
- debe expresar un caso de uso concreto;
- sus dependencias y cleanup siguen importando.

No conviertas cualquier helper en Hook. Si una función no usa Hooks, debe ser
una función normal.

## Práctica

¿Necesita Effect `const total = price * quantity`?

<details>
<summary>Ver respuesta</summary>

No. Es un valor derivado que puede calcularse durante cada render.

</details>
