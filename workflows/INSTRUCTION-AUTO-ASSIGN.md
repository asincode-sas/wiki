# Crear Workflow para Auto Asignar Revisores

Si el archivo `.github/workflows/auto-assign.yaml` no existe en el repositorio, créalo con el siguiente contenido:  

```yaml
name: Auto Assign PR

on:
  pull_request:
    types: [opened]

jobs:
  trigger:
    uses: asincode-sas/actions/.github/workflows/pr-auto-assign.yaml@main
