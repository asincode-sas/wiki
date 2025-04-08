# Error: The type 'JSX' is undefined

Este error aparece generalmente cuando se utiliza `JSX.Element` en una anotación de tipo en JSDoc, sin que el entorno esté correctamente configurado para reconocer los tipos globales de React.

Mensaje: 

```bash
The type 'JSX' is undefined.
```

## Causa

En algunos entornos, especialmente cuando se trabaja con JSDoc en proyectos el tipo JSX.Element no se reconoce automáticamente, ya que JSX no está disponible en el ámbito global.

## Solución ✅

Para solucionar el problema, debes reemplazar JSX.Element en tu JSDoc por `import('react').JSX.Element`. Esto garantiza que el tipo se importe explícitamente desde React.

### Antes

```javascript
/**
 * @returns {JSX.Element}
 */
function MyComponent() {
  return <div>Hello</div>;
}
```

### Después

```javascript
/**
 * @returns {import('react').JSX.Element}
 */
function MyComponent() {
  return <div>Hello</div>;
}
```
