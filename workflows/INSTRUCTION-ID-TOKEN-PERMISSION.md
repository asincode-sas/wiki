# Agregar Permiso id-token en Workflow de Coverage

Si en `.github/workflows/unit-testing.yaml` no está definido el permiso `id-token`, agrega lo siguiente:  

```yaml

...
permissions:
  id-token: write
  contents: read
...


```
