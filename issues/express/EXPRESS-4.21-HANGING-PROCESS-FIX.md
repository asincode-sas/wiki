# Solución al error de Express con pruebas colgadas

Al ejecutar las pruebas, el proceso queda colgado indefinidamente. Para solucionarlo, es necesario ajustar la configuración en los archivos `test/setupTest.js` y la propiedad `lint-staged` en el archivo `package.json`.

## Paso 1 - Ajustar el archivo `test/setupTest.js`

Si el archivo no existe, créalo y agrega la siguiente línea para definir el entorno de prueba:

```javascript
process.env.NODE_ENV = "test";
```

## Paso 2 - Modificar `lint-staged` en `package.json`

La configuración de pruebas debe quedar asì: `npx c8 node --import ./test/setupTest.js --test`

Ejemplo en el archivo package.json

```json
"lint-staged": {
  "*.{js,ts}": [
    "npx previous command",
    "npx c8 node --import ./test/setupTest.js --test"
  ]
}
```

Estos cambios evitarán que las pruebas queden colgadas.