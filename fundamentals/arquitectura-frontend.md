---
title: Arquitectura frontend
status: generated
tags: [architecture, frontend, clean-architecture, screaming-architecture]
related:
  - ../technologies/react/patrones-de-componentes.md
  - ../languages/typescript/modelado-de-datos.md
sources:
  - https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
  - https://blog.cleancoder.com/uncle-bob/2011/11/22/Clean-Architecture.html
updated: 2026-06-08
---

# Arquitectura frontend

> La arquitectura debe hacer visible el negocio y controlar las dependencias,
> no producir carpetas ceremoniales.

## Screaming Architecture

La estructura del proyecto debería "gritar" qué hace el producto. Una app de
seguros debería mostrar conceptos como `policies`, `claims` y `customers`, no
solo carpetas técnicas como `components`, `hooks` y `services`.

```text
src/
  features/
    policies/
    claims/
    customers/
  shared/
```

Es una orientación por dominio o feature. No define por sí sola cómo se
comunican las capas.

## Clean Architecture

Busca separar reglas de negocio de detalles externos como React, HTTP,
almacenamiento o una librería de estado. La regla central es que las
dependencias apunten hacia el conocimiento más estable del negocio.

Una adaptación frontend razonable:

```text
features/orders/
  domain/
  application/
  infrastructure/
  ui/
```

No todas las features necesitan las cuatro carpetas. En una pantalla CRUD
pequeña puede ser exceso de diseño.

## Container y Presentational

Es un patrón de componentes, no una API de React:

- Container: obtiene datos y coordina comportamiento.
- Presentational: recibe props y representa UI.

```tsx
function UserPage() {
  const user = useUser();
  return <UserProfile user={user} />;
}
```

Los custom hooks reducen la necesidad de containers dedicados, pero la
separación entre coordinación y presentación sigue siendo útil.

## Combinación práctica

Una estructura feature-first puede aplicar las tres ideas:

```text
features/
  checkout/
    api/
    components/
    hooks/
    model/
    pages/
```

- "Screaming": `checkout` comunica el dominio.
- "Clean": `model` no depende de los componentes.
- Container/presentational: páginas y hooks coordinan; componentes presentan.

## Cuándo no usar capas completas

- Prototipo de corta vida.
- Feature con una sola vista y reglas triviales.
- Separaciones que solo mueven código sin reducir acoplamiento.

Empieza simple y extrae límites cuando aparezcan reglas, cambios frecuentes,
dependencias externas o necesidad real de pruebas aisladas.

## Práctica

¿Qué comunica mejor el negocio: `src/services/order-service.ts` o
`src/features/checkout/api/create-order.ts`?

<details>
<summary>Ver respuesta</summary>

La segunda ruta hace visible el caso de uso y mantiene el detalle HTTP dentro
de la feature. No siempre será la única estructura válida, pero expresa mejor
la intención.

</details>
