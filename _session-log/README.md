# 🗒️ Session Log

> Bitácora de sesiones de programación. Aquí capturo en bruto lo que aprendí cada sesión — comandos nuevos, tecnos descubiertas, errores resueltos. Después decido qué merece su propio doc en otra carpeta.

---

## 🚀 Cómo usar esto

### Al final de cada sesión (2-3 min)

1. Crea un archivo `YYYY-MM-DD.md` en esta carpeta (un archivo por sesión, o uno por día).
2. Anota en bullets crudos lo que aprendiste — no tiene que estar bonito.
3. Marca con `→ promover` lo que merezca convertirse en un doc formal después.

### Plantilla mínima de entrada

```markdown
# 2026-05-12 · Lo que aprendí hoy

**Proyectos tocados:** The-Dev-Guide, geriaCare
**Estado mental:** productivo / atorado / explorando

## Tecnos nuevas
- ...

## Comandos / atajos que voy a querer volver a usar
- ...

## Errores que me costaron y cómo los resolví
- ...

## Para documentar formalmente después → promover
- [ ] tema X → `0N-categoria/nombre.md`

## Notas sueltas
- ...
```

---

## 🤖 Con Claude Code

Al final de la sesión, pídele:

> "Organiza lo que aprendí hoy en el repo según las convenciones. Si algo merece un doc nuevo, créalo usando `_templates/plantilla-doc.md`. Si solo es una nota suelta, agrégala al session-log de hoy."

Claude leerá esta carpeta y los docs existentes para decidir dónde va cada cosa. **Siempre revisa el diff antes de hacer commit.**

---

## 📐 Reglas

- Un archivo por sesión (o por día). Nombre: `YYYY-MM-DD.md`.
- Bullets crudos están bien — no es para publicar, es para acordarte.
- Cuando un tema del session-log se vuelva un doc formal, marca el bullet como `✅ promovido → ruta/al/doc.md` en lugar de borrarlo. Así queda el rastro.
- Cada cierto tiempo (mes/trimestre), archiva sesiones viejas en `_session-log/archive/YYYY/`.
