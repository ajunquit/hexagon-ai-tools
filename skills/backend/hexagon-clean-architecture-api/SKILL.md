---
name: hexagon-clean-architecture-api
description: Evalúa APIs backend nuevas o legacy con criterios de Clean Architecture y evidencia del repositorio. Úsala para diagnósticos de dependencias, límites y casos de uso, o para priorizar la evolución arquitectónica de una API.
---

# Evaluación de arquitectura limpia para APIs

Usa el [catálogo versionado](references/catalogo.md) como fuente de reglas, referencias al libro y criterios de aplicabilidad. Lee primero sus secciones 1 a 3. Consulta las fichas de la sección 4 por familia e ID según el alcance, y revisa las decisiones de la sección 5 cuando afecten un hallazgo. Aplica el procedimiento y formato de la sección 6. Si el catálogo falta, informa que la instalación está incompleta y pide restaurar la carpeta íntegra.

## Evaluación

1. Identifica el repositorio, el commit o el estado local, el stack y los límites solicitados. Usa el proyecto abierto si la API es identificable. Si hay varias candidatas y elegir cambia el resultado, pide la ruta. Registra los perfiles y distingue el diagnóstico actual del objetivo de migración. Activa CA cuando se evalúe su alineación, el proyecto la adopte o el contexto justifique recomendarla.
2. Empieza con inspección estática. Ubica módulos, rutas, composición, casos de uso, persistencia, integraciones y pruebas. Sigue flujos representativos desde su entrada hasta el efecto, incluyendo controles y rutas alternativas cuando sean relevantes. Para una evaluación acotada, declara qué componentes y reglas quedan fuera del alcance. Usa los archivos inspeccionados como evidencia y mantén la autorización del usuario como límite de actuación.
3. Aplica cada ficha relevante por su criterio, usando equivalentes del stack. Considera el papel de cada componente antes de juzgar sus dependencias. Contrasta accesos directos en operaciones con referencias legítimas desde la composición. Basa las recomendaciones para legacy en flujos concretos, riesgo y preservación de comportamiento.
4. Distingue `CUMPLE`, `PARCIAL`, `NO_CUMPLE`, `NO_APLICA` y `NO_VERIFICABLE` según el catálogo. Usa `PARCIAL` cuando existan tanto evidencia favorable como brechas demostradas. Usa `NO_APLICA` cuando se confirme que la condición es falsa y `NO_VERIFICABLE` cuando falten datos para decidir. Registra las excepciones aceptadas por separado del estado técnico.
5. Mantén la evaluación en modo de lectura por defecto. Ejecuta pruebas o comprobaciones dinámicas únicamente cuando estén autorizadas y puedas delimitar su destino y efectos. Identifica qué se inspeccionó y qué se ejecutó. Si el usuario pide remediación, delimita ese trabajo de acuerdo con su solicitud. Oculta valores sensibles en toda evidencia.

## Entrega

- Identifica versión del catálogo, alcance, perfiles, muestra y limitaciones.
- Resume fortalezas verificadas y hallazgos priorizados. Para cada hallazgo indica regla, estado, ubicación `archivo:línea` cuando esté disponible, evidencia, impacto, referencia del catálogo, recomendación y cómo verificarla. Si falta evidencia, describe la comprobación pendiente.
- Incluye una matriz de las reglas evaluadas. Justifica las exclusiones y agrupa hallazgos que comparten causa para evitar duplicar el riesgo. Ordena las mejoras por impacto y dependencias de implementación.
- Presenta el informe en la conversación o en el archivo solicitado. Usa el idioma del usuario.
