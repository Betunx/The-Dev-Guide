---
title: React Hook Form
status: generated
tags: [react-hook-form, forms, validation, zod, yup]
related:
  - ../react/estado-y-comunicacion.md
  - ../../languages/typescript/modelado-de-datos.md
sources:
  - https://react-hook-form.com/docs/useform
  - https://github.com/react-hook-form/resolvers
  - https://zod.dev/
  - https://github.com/jquense/yup
updated: 2026-06-08
---

# React Hook Form

> React Hook Form administra valores, validación y estado de formularios
> procurando reducir renders y aprovechar inputs nativos.

## `useForm`

```tsx
type FormValues = {
  email: string;
  age: number;
};

const {
  register,
  handleSubmit,
  formState: { errors, isSubmitting },
} = useForm<FormValues>();
```

- `register`: conecta un input.
- `handleSubmit`: valida y entrega datos.
- `formState`: errores, dirty, touched, submitting y otros estados.
- `reset`: restaura valores.
- `setValue` y `getValues`: acceso imperativo puntual.
- `watch`/`useWatch`: observación de valores.

```tsx
<form onSubmit={handleSubmit(onSubmit)}>
  <input {...register("email", { required: true })} />
  {errors.email && <p>El email es obligatorio</p>}
</form>
```

## Componentes controlados

Para componentes externos que no exponen una interfaz de input nativo, usa
`Controller` o `useController`.

No conviertas todos los inputs en controlados sin necesidad.

## Validación con schema

Los resolvers conectan librerías como Zod y Yup:

```tsx
const schema = z.object({
  email: z.string().email(),
  age: z.coerce.number().int().min(18),
});

type FormValues = z.infer<typeof schema>;

const form = useForm<FormValues>({
  resolver: zodResolver(schema),
});
```

## Zod vs Yup

| Aspecto | Zod | Yup |
|---|---|---|
| Enfoque TypeScript | inferencia central | soporte de inferencia |
| API | schemas inmutables | schemas con estilo fluent |
| Ecosistema | muy común en TS moderno | maduro y ampliamente usado |

La mejor elección puede depender del proyecto y sus dependencias existentes.
Ambas validan en runtime, algo que TypeScript solo no puede hacer.

## Buenas prácticas

- Define `defaultValues` de forma consistente.
- Modela el tipo del formulario.
- Muestra errores cerca del campo y de forma accesible.
- Separa validación de interfaz y reglas reales del servidor.
- El servidor debe volver a validar datos.
- Evita observar todo el formulario si solo necesitas un campo.

## Práctica

¿Por qué usar Zod si el formulario ya tiene un tipo TypeScript?

<details>
<summary>Ver respuesta</summary>

Porque TypeScript desaparece al compilar. Zod valida valores reales durante la
ejecución y puede inferir el tipo estático desde el mismo schema.

</details>

