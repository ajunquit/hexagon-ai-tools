# Instalar la skill en Codex y Claude Code

Necesitas Git, el agente que quieras utilizar y una copia del repositorio `hexagon-ai-tools`. Para obtenerla en GitHub, usa **Code → HTTPS** y clona la URL que muestra GitHub. También puedes usar una copia local del repositorio.

La carpeta que debes copiar es `skills/backend/hexagon-clean-architecture-api/`. Incluye `SKILL.md` y `references/catalogo.md`. Usa un destino por agente y alcance para evitar instalaciones duplicadas.

| Agente | Solo para el proyecto de la API | Para tu usuario |
| --- | --- | --- |
| Codex | `<raíz-api>/.agents/skills/` | `~/.agents/skills/` |
| Claude Code | `<raíz-api>/.claude/skills/` | `~/.claude/skills/` |

Las rutas corresponden a instalaciones locales. Consulta la [documentación oficial de skills de Codex](https://developers.openai.com/codex/skills#where-to-save-skills) y la [documentación oficial de skills de Claude Code](https://code.claude.com/docs/en/skills#choose-where-skills-load).

## Windows con PowerShell

Abre PowerShell en la raíz del repositorio de la API. Ajusta `$toolkit` a la ruta real de tu copia de `hexagon-ai-tools`. Este bloque instala la skill en el proyecto para ambos agentes. Para instalarla para tu usuario, cambia `$scopeRoot` por `$HOME`. Si ya existe una copia, el bloque la conserva.

```powershell
$toolkit = 'C:\ruta\a\hexagon-ai-tools'
$scopeRoot = (Get-Location).Path
$name = 'hexagon-clean-architecture-api'
$source = Join-Path $toolkit "skills/backend/$name"

if (!(Test-Path -LiteralPath (Join-Path $source 'SKILL.md') -PathType Leaf) -or
    !(Test-Path -LiteralPath (Join-Path $source 'references/catalogo.md') -PathType Leaf)) {
    throw "Carpeta de origen incompleta. Revisa la ruta: $source"
}

foreach ($relativeDir in @('.agents/skills', '.claude/skills')) {
    $skillsDir = Join-Path $scopeRoot $relativeDir
    $target = Join-Path $skillsDir $name
    if (Test-Path -LiteralPath $target) {
        Write-Warning "Copia existente conservada: $target"
        continue
    }
    New-Item -ItemType Directory -Path $skillsDir -Force | Out-Null
    Copy-Item -LiteralPath $source -Destination $target -Recurse -ErrorAction Stop
}
```

## macOS y Linux

Abre la terminal en la raíz de la API y ajusta `toolkit`. Para instalar la skill para tu usuario, cambia `scope_root` por `"$HOME"`. El bloque funciona en un shell POSIX y conserva copias existentes.

```sh
(
  set -eu
  toolkit='/ruta/a/hexagon-ai-tools'
  scope_root="$PWD"
  name='hexagon-clean-architecture-api'
  source_dir="$toolkit/skills/backend/$name"

  if [ ! -f "$source_dir/SKILL.md" ] || [ ! -f "$source_dir/references/catalogo.md" ]; then
    printf 'Carpeta de origen incompleta: %s\n' "$source_dir" >&2
    exit 1
  fi

  for relative_dir in .agents/skills .claude/skills; do
    skills_dir="$scope_root/$relative_dir"
    target="$skills_dir/$name"
    if [ -e "$target" ] || [ -L "$target" ]; then
      printf 'Copia existente conservada: %s\n' "$target"
      continue
    fi
    mkdir -p "$skills_dir"
    cp -R "$source_dir" "$target"
  done
)
```

En ambos bloques, puedes conservar solo el destino del agente que utilizas.

## Invocar y comprobar

Abre una sesión en el proyecto de la API. Si la skill no aparece en el selector, comprueba la ruta y abre una sesión nueva.

- **Codex CLI o IDE.** Selecciona la skill con `$` o `/skills` y envía la petición. En la app de escritorio, búscala en el selector de skills. [Documentación oficial de invocación](https://developers.openai.com/codex/skills#how-codex-uses-skills)

  ```text
  $hexagon-clean-architecture-api Evalúa la alineación de esta API legacy. Empieza por pedidos y entrega hallazgos con archivo y línea.
  ```

- **Claude Code.** Usa el comando `/hexagon-clean-architecture-api` en la sesión abierta sobre la API. [Documentación oficial de skills de Claude Code](https://code.claude.com/docs/en/skills)

  ```text
  /hexagon-clean-architecture-api Evalúa la alineación de esta API legacy. Empieza por pedidos y entrega hallazgos con archivo y línea.
  ```

Comprueba que el informe identifica la versión del catálogo, el alcance y los perfiles, y que cita IDs de reglas como `CA-APP-001` junto a la evidencia. Una ruta de negocio inaccesible debe figurar con la limitación correspondiente.

## Actualizar o retirar

Actualiza tu copia del repositorio y revisa los cambios en `SKILL.md` y en el catálogo. Si quieres actualizar una instalación, mueve primero la carpeta instalada a un respaldo fuera del directorio de skills y vuelve a ejecutar la copia. Para retirarla, mueve esa misma carpeta fuera de los destinos elegidos. Abre una sesión nueva para comprobar qué versión se carga.
