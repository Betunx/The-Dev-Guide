---
title: Modelado de datos con TypeScript
status: generated
tags: [typescript, modeling, types, dto]
related:
  - ../../technologies/react/typescript-en-react.md
  - ../../technologies/react-hook-form/README.md
sources:
  - https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
  - https://www.typescriptlang.org/docs/handbook/2/narrowing.html
  - https://www.typescriptlang.org/docs/handbook/2/objects.html
updated: 2026-06-08
---

# Modelado de datos con TypeScript

> Modelar consiste en representar estados válidos y hacer difíciles los
> estados imposibles.

## Tipo de dominio y DTO

La forma recibida por una API no siempre debe circular por toda la aplicación.

```ts
type UserDto = {
  id: string;
  created_at: string;
};

type User = {
  id: string;
  createdAt: Date;
};

function toUser(dto: UserDto): User {
  return {
    id: dto.id,
    createdAt: new Date(dto.created_at),
  };
}
```

El mapper crea una frontera entre infraestructura y dominio.

## Uniones discriminadas

Evitan combinaciones contradictorias como `loading: true` junto con `data`.

```ts
type RequestState<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };
```

Al evaluar `status`, TypeScript estrecha el tipo disponible.

## `type` e `interface`

- `interface`: buena para contratos de objetos extensibles.
- `type`: buena para uniones, intersecciones, alias y composición.

No es necesario imponer una guerra de estilos. Usa una convención consistente.

## Reglas útiles

- Prefiere `unknown` sobre `any` en fronteras externas.
- Valida en runtime datos de red, formularios y almacenamiento.
- Usa `readonly` cuando una función no debería mutar una entrada.
- Nombra por significado: `UserId`, `Money`, `OrderStatus`.
- Representa ausencia conscientemente con `null` o `undefined`.
- No uses opcionales para esconder que existen varios estados distintos.

TypeScript comprueba durante desarrollo; no valida JSON en ejecución. Para eso
se necesita código de validación o un schema como Zod o Yup.

## Práctica

Modela una petición que puede estar cargando, fallar o terminar con una lista de
usuarios, evitando booleanos contradictorios.

<details>
<summary>Ver respuesta</summary>

Usa una unión discriminada como `RequestState<User[]>` y renderiza mediante un
`switch` sobre `status`.

</details>
