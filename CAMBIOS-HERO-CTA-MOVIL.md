# Mejora del CTA del hero en móvil

## ✅ Cambio implementado

El botón "Prueba gratis" del hero (`#inicio`) ahora se muestra **centrado y abajo** en teléfono.

### Antes (móvil)
- La píldora CTA ("Comienza a optimizar tu obra" + botón) quedaba alineada a la izquierda.
- Texto y botón en fila se desbordaban en pantallas de 390px (texto ~190px + botón ~130px > espacio disponible).

### Después (móvil, < 640px)
- Píldora a **ancho completo** (`w-full`) con contenido **centrado** y apilado en columna: texto arriba, botón debajo.
- Botón a lo ancho (`w-full`), más alto (`h-11`) y con mayor área táctil (`px-8`).
- Esquinas `rounded-3xl` para la píldora apilada.
- El conjunto queda apoyado al fondo del hero (el contenedor padre ya usa `justify-end`).

### Escritorio (>= 640px)
- Sin cambios: píldora horizontal `rounded-full` con texto y botón en fila, ancho automático, botón `h-10 px-6`.

## 🔧 Clases aplicadas

```html
<!-- Contenedor CTA -->
flex flex-col sm:flex-row items-center gap-3 sm:gap-4
rounded-3xl sm:rounded-full ... px-6 py-4 sm:py-3
w-full sm:w-auto

<!-- Botón -->
h-11 sm:h-10 w-full sm:w-auto px-8 sm:px-6
```

## 📱 Verificado en navegador

- Móvil (390px): botón centrado (centro X 195 = centro del hero), 276px de ancho, 44px de alto, al fondo del hero.
- Escritorio (1280px): píldora en fila de 397px, botón 138×40px, radio completo — idéntico al diseño anterior.
