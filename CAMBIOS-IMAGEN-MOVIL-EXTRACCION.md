# Imagen responsiva en "Extracción IA de documentos"

## ✅ Cambio implementado

La tarjeta destacada "Extracción IA de documentos" (sección `#solucion` de `index.html`) ahora soporta **una imagen distinta para celular y otra para tablet/escritorio**.

### Cómo funciona

| Pantalla | Imagen | Elemento |
|---|---|---|
| Celular / iPhone (< 768px) | `images/extraccion-ia-movil.jpg` | `<img>` con `md:hidden` |
| Tablet / escritorio (≥ 768px) | `images/extraccion-ia.jpg` | `div` con fondo, `hidden md:block` |

### Fallback seguro

- Si `images/extraccion-ia-movil.jpg` **no existe todavía**, el atributo `onerror` cambia automáticamente a `images/extraccion-ia.jpg` (la de escritorio). La tarjeta nunca se ve rota.
- Para activar la imagen de celular solo hay que **agregar el archivo** `images/extraccion-ia-movil.jpg` (idealmente vertical/cuadrado, ej. 1080×1350) — sin tocar código.

### Nota

- No se detecta el dispositivo (iPhone vs Android): se usa el ancho de pantalla (`md:` = 768px), que es la práctica estándar y funciona igual en cualquier teléfono.
- El efecto `group-hover:scale-105` y la opacidad se conservan en ambas imágenes.
- El mismo patrón se puede replicar en las demás tarjetas (ej. "Extracción IA de documentos." del carrusel de beneficios) si se desea.

## 📱 Verificado en navegador

- Móvil (390px): `<img>` visible; al no existir `extraccion-ia-movil.jpg`, el fallback cargó `extraccion-ia.jpg` correctamente.
- Escritorio (1280px): `<img>` oculto y el `div` de fondo con `extraccion-ia.jpg` visible, como siempre.
