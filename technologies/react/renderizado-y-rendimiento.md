---
title: Renderizado y rendimiento en React
status: generated
tags: [react, rendering, strict-mode, memo, performance]
related:
  - react-19-y-compiler.md
  - efectos-referencias-y-custom-hooks.md
sources:
  - https://react.dev/learn/render-and-commit
  - https://react.dev/reference/react/StrictMode
  - https://react.dev/reference/react/memo
  - https://react.dev/reference/react/useMemo
  - https://react.dev/reference/react/useCallback
  - https://react.dev/reference/react/useRef
updated: 2026-06-08
---

# Renderizado y rendimiento en React

> Un rerender es una nueva ejecución del componente para calcular UI; no es
> necesariamente una modificación del DOM ni un problema de rendimiento.

## Ciclo mental

1. Trigger: montaje o actualización.
2. Render: React ejecuta componentes y calcula la salida.
3. Commit: aplica al DOM las diferencias.
4. Effects: se sincronizan después del commit según su tipo.

## Qué provoca renders

- Estado propio actualizado.
- Render de un ancestro.
- Context consumido que cambia.
- Suscripción a un store externo.
- Cambio de identidad mediante `key`, que puede remontar el componente.

Actualizar con el mismo valor según `Object.is` puede permitir que React omita
trabajo. Un padre renderizado suele provocar el render de sus hijos, salvo que
una optimización permita saltarlo.

## Strict Mode

En desarrollo, Strict Mode realiza comprobaciones adicionales:

- ejecuta renders extra para detectar impureza;
- repite el ciclo setup/cleanup de Effects;
- repite callbacks de refs;
- muestra advertencias por APIs deprecadas.

No ocurre igual en producción. La solución no es desactivar Strict Mode para
ocultar duplicados, sino hacer renders puros y Effects con cleanup correcto.

## `memo`

Memoiza un componente y normalmente permite omitir su render si sus props no
cambiaron.

```tsx
const Row = memo(function Row({ item }: Props) {
  return <li>{item.name}</li>;
});
```

Es optimización, no garantía. El estado propio y Context todavía pueden
provocar renders.

## `useMemo`

Memoriza el resultado de un cálculo:

```tsx
const visibleItems = useMemo(
  () => filterItems(items, query),
  [items, query],
);
```

Úsalo para cálculos medidos como costosos o para conservar identidad cuando
esa identidad importa. No arregla lógica incorrecta.

## `useCallback`

Memoriza la identidad de una función:

```tsx
const handleSelect = useCallback((id: string) => {
  selectItem(id);
}, [selectItem]);
```

Ayuda cuando la función se entrega a un componente memoizado o es dependencia
de otro Hook. Crear funciones durante render es normal.

## `useRef`

Conserva un valor entre renders sin provocar uno al modificar `current`.

```tsx
const inputRef = useRef<HTMLInputElement>(null);
```

Sirve para nodos DOM, identificadores de timers o valores imperativos. No debe
reemplazar estado que necesita aparecer en la UI.

## Cómo evitar renders innecesarios

Antes de memoizar:

- mantén estado local;
- usa composición con `children`;
- elimina Effects que actualizan estado sin necesidad;
- evita Context monolítico;
- pasa props primitivas cuando sea natural;
- mide con React DevTools Profiler.

Después, aplica `memo`, `useMemo` o `useCallback` en el punto medido.

## Tabla

| API | Conserva | Provoca render al cambiar |
|---|---|---|
| `memo` | resultado del componente según props | depende del componente |
| `useMemo` | valor calculado | no por sí mismo |
| `useCallback` | función | no por sí mismo |
| `useRef` | contenedor mutable | no |

## Práctica

Un componente renderiza porque su padre cambió, pero el DOM queda igual.
¿React falló?

<details>
<summary>Ver respuesta</summary>

No. Render y commit son fases distintas. React puede recalcular la salida y
descubrir que no necesita modificar el DOM.

</details>

