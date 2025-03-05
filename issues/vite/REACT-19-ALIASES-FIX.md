# Solución al error de React 19 con Vite y los alias al ejecutar las pruebas

Para solucionar este problema, es necesario realizar ajustes en la configuración de `jsconfig.json`, modificar `vite.config.js` e instalar el paquete `vite-tsconfig-paths`.

## 1. Ajustar `jsconfig.json`

Asegúrate de que tu archivo `jsconfig.json` contenga las configuraciones adecuadas para los alias:

```json
// jsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "module": "ESNext",
    "types": [
      "vitest/globals"
    ],
    "paths": {
      "@app": [
        "src/App.jsx"
      ],
      "@router": [
        "src/router.jsx"
      ],
      "@*": [
        "src/*"
      ],
    }
  }
}
```

## 2. Instalar `vite-tsconfig-paths`

Ejecuta el siguiente comando para instalar el paquete necesario:

```sh
# Usando npm
npm i -D vite-tsconfig-paths
```

## 3. Modificar `vite.config.js`

Asegúrate de importar y usar `vite-tsconfig-paths` en la configuración de Vite:

```js
// vite.config.js
import { coverageConfigDefaults, defineConfig } from 'vitest/config';
import react from '@vitejs/plugin-react';
import tsconfigPaths from 'vite-tsconfig-paths'

// https://vite.dev/config/
export default defineConfig(({ mode }) => ({
  esbuild: {
    drop: mode === 'production' ? ['console', 'debugger'] : [],
  },
  plugins: [
    react(),
    tsconfigPaths(),
  ],
  test: {
    setupFiles: './test/setupTest.js',
    global: true,
    environment: 'jsdom',
    reporters: process.env.GITHUB_ACTIONS ? ['github-actions'] : ['dot'],
    coverage: {
      lcovReportDir: 'coverage/lcov-report',
      all: true,
      reporter: ['text', 'lcov'],
      exclude: [
        '**/*.config.*',
        '**/index.js',
        'html/**',
        'src/data/**',
        'src/main.jsx',
        'test/**',
        'public/**',
        ...coverageConfigDefaults.exclude,
      ],
    },
  },
}));
```

| Si hay algún plugin adicional o configuración, no olvides agregarlo ya que cada repo puede usar diferentes plugins.

Con estos cambios, los alias deberían funcionar correctamente con React 19 en Vite.

