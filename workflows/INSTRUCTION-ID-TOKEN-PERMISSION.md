# Agregar Permiso id-token en Workflow de Coverage

Si en `.github/workflows/test-node.yaml` no está definido el permiso `id-token`, agrega lo siguiente:  

```yaml

...
permissions:
  id-token: write
  contents: read
...


```
