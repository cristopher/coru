# Corrección de proporción de tarjetas en "Automatiza lo que hoy haces a mano"

## ✅ Cambio implementado

Las tarjetas del carrusel en la sección `#beneficios` ahora tienen proporciones correctas en teléfono, siguiendo el estilo Apple de la referencia.

### Antes (móvil, 390px)
- Tarjeta: `w-[50vw]` = 195px — demasiado angosta
- Imagen: `aspect-video` (16:9) = 195×109px — muy achatada
- Texto: `text-2xl` (24px) — grande para el poco espacio
- Resultado: tarjetas alargadas con imagen aplastada

### Después (móvil, 390px)
- Tarjeta: `w-[75vw]` = 293px — ancho suficiente para contenido
- Imagen: `aspect-[4/3]` (ratio 1.33) = 293×220px — proporción cuadrada/cuboide
- Texto: `text-xl` (20px) — proporcional al espacio
- Gap reducido a `gap-5` / `px-5`
- Peek de la siguiente tarjeta visible a la derecha

### Escritorio (≥ 768px)
- Tarjeta: `md:w-[40vw]` / `lg:w-[30vw]` — 3 tarjetas por fila
- Imagen: `aspect-[4/3]` — misma proporción
- Texto: `md:text-2xl` (24px)

## � Bug corregido: flechas al inicio/fin del carrusel

### Problema
Al llegar al inicio o al final del carrusel usando las flechas en móvil, el scroll continuaba más allá de los límites, mostrando espacio vacío. Las flechas no se deshabilitaban.

### Causas
1. **Gap hardcodeado incorrecto**: el código usaba `cardWidth + 32` (para `gap-8`), pero el carrusel tenía `gap-5` (20px)
2. **Sin detección de límites**: las flechas no se deshabilitaban al inicio/fin

### Solución
- Corregido el gap a `cardWidth + 20` para coincidir con `gap-5`
- Agregada función `updateCarouselButtons()` que detecta el scroll position
- Flechas se deshabilitan con `opacity-30` y `pointer-events-none` al llegar a los límites
- Recálculo automático en scroll, window load y timeout post-render

### Test Results (móvil 390px)
| Estado | prev | next | scrollLeft |
|---|---|---|---|
| Inicio | ❌ disabled | ✅ enabled | 0 |
| Mitad | ✅ enabled | ✅ enabled | 284 |
| Final | ✅ enabled | ❌ disabled | 568 |
| Vuelta al inicio | ❌ disabled | ✅ enabled | 0 |

### Test Results (desktop 1280px)
- Inicio: prev disabled, next enabled, maxScroll=72px ✓

## �📊 Comparativa

| Propiedad | Antes (móvil) | Después (móvil) | Referencia Apple |
|---|---|---|---|
| Ancho tarjeta | 195px (50vw) | 293px (75vw) | ~80vw |
| Ratio imagen | 16:9 (1.78) | 4:3 (1.33) | ~1:1 a 4:3 |
| Alto imagen | 109px | 220px | ~250-300px |
| Font título | 24px | 20px | compacto |
| Peek siguiente | barely visible | visible | sí |

## 📱 Verificado

- Móvil (390px): proporción correcta, peek visible, texto compacto ✓
- Escritorio (1280px): 3 tarjetas de 384px, misma proporción 4:3 ✓
- Sin errores en el archivo ✓
