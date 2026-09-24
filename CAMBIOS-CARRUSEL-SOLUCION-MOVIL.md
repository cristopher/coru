# Carrusel móvil para "El costo oculto de la gestión manual"

## ✅ Cambio implementado

En teléfonos (< 768px) la sección `#solucion` de `index.html` ahora se comporta como un carrusel estilo Apple, igual al de la referencia:

- **Tarjetas a ancho completo**: cada tarjeta ocupa `85vw` con un asomo de la siguiente (`px-[7.5vw]` en el contenedor).
- **Indicador inferior de puntos**: 3 puntos dentro de una píldora; el activo se alarga (`w-6`) y oscurece. Solo visible en móvil (`md:hidden`).
- **Swipe con el dedo**: scroll nativo con `snap-x snap-mandatory`; los puntos se sincronizan con la posición del scroll.
- **Auto-avance**: cada 4 segundos pasa a la siguiente tarjeta y vuelve al inicio en loop.

## 🔧 Implementación

### HTML
- El contenedor del bento grid pasó de `grid grid-cols-1 md:grid-cols-12` a `flex md:grid md:grid-cols-12` con `overflow-x-auto snap-x snap-mandatory hide-scrollbar` (en `md:` vuelve a `overflow-visible`).
- Cada tarjeta lleva la clase `solucion-slide` más `w-[85vw] md:w-auto shrink-0 snap-center md:snap-none`.
- La columna derecha (`md:col-span-5`) usa `display: contents` en móvil (`contents md:flex md:flex-col md:gap-6 md:col-span-5`) para que sus 2 tarjetas se conviertan en slides independientes sin duplicar HTML. En escritorio el bento grid queda idéntico.
- Alturas iguales en móvil: `min-h-[64vw] md:min-h-0` en las tarjetas 2 y 3.
- Los puntos se generan por JS en `#solucion-dots` (un `button` por tarjeta, con `role="tab"` y `aria-label`).

### JavaScript (dentro del `DOMContentLoaded` existente)
- `goToSlide(index)`: centra la tarjeta con `scrollTo` suave y actualiza puntos.
- Scroll del contenedor (rAF): detecta la tarjeta más cercana al centro → sincroniza puntos; al estabilizarse (200ms) reanuda el autoplay.
- Autoplay (`setInterval` 4000ms) que se pausa cuando:
  - el usuario está tocando el carrusel (`touchstart` / `pointerdown`),
  - la sección no está visible (`IntersectionObserver`, threshold 0.3),
  - la pestaña está en segundo plano (`document.hidden`),
  - el viewport es ≥ 768px (escritorio no tiene autoplay).
- Clic en un punto: salta a esa tarjeta y reanuda el autoplay.
- `resize`: recentra la tarjeta actual sin animación.

## 📱 Verificado en navegador

- Móvil (390px): tarjetas de 332px (85vw), scroll horizontal con snap, 3 puntos visibles, swipe sincroniza puntos, autoplay avanza y hace loop.
- Escritorio (921px): bento grid intacto (col-span-7 / col-span-5), puntos ocultos, sin scroll horizontal.

## Nota de testing

El navegador integrado reporta `document.hidden = true` (pestaña en segundo plano): el autoplay queda pausado por diseño y el scroll suave se congela. Para probarlo, usar un navegador en primer plano o simular tocando el carrusel.
