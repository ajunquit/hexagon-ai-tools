# Hexagon AI Tools

Colección de skills y utilidades para agentes de desarrollo. La primera skill evalúa APIs backend con un catálogo versionado de arquitectura limpia y produce hallazgos trazables al código.

| Skill | Propósito | Agentes |
| --- | --- | --- |
| [hexagon-clean-architecture-api](skills/backend/hexagon-clean-architecture-api/SKILL.md) | Diagnosticar una API nueva o legacy y priorizar mejoras con evidencia. | Codex y Claude Code |

[Guía de instalación y uso](docs/instalacion.md)

## Organización

- `skills/backend/` reúne las skills de backend. Cada carpeta contiene su `SKILL.md` y las referencias que necesita.
- `skills/frontend/` es la ruta reservada para futuras skills de frontend. Se creará con la primera incorporación.
- `skills/<area>/` admite nuevas áreas conforme se incorporen herramientas.
- [`hooks/`](hooks/README.md) documenta cómo incorporar hooks por agente.
- `docs/` contiene las guías de instalación y uso de la colección.

Codex y Claude Code consumen la misma carpeta de la skill. El [catálogo](skills/backend/hexagon-clean-architecture-api/references/catalogo.md) conserva la procedencia de las reglas, las adaptaciones a APIs y la política de evaluación.
