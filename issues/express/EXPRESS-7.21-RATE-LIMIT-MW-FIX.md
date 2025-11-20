# Solución a la configuración de express-rate-limit

Este documento describe los pasos para actualizar el middleware de limitación (`limiter`) a **express-rate-limit v7+**, solucionando el error 
```javascript
**ValidationError: Unexpected configuration option: windowMS**
**code: 'ERR_ERL_UNKNOWN_OPTION'**
```
## Paso 1 - Actualizar el middleware `limiter`

1. Cambiar el import a **nombrado** en `src/middlewares/limit.middleware.js`:

```javascript
import { LIMIT, LIMIT_MESSAGE } from '#config/environment.config';
import { rateLimit } from 'express-rate-limit';
```
Modificar la función limiter para usar las opciones correctas de la versión 7+:

```javascript
export const limiter = (skip = false) => rateLimit({
  skip: () => skip,                  
  windowMs: 30 * 1000,               // Corrección: usar "windowMs" con 's' minúscula
  limit: LIMIT,
  message: LIMIT_MESSAGE,
  legacyHeaders: false,             
});
```
