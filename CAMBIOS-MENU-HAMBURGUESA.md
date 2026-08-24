# Cambios: Menú hamburguesa estilo Apple

## Objetivo
Ocultar el menú de la navbar superior en móvil y reemplazarlo por un menú hamburguesa que funciona como el de apple.com: pantalla completa oscura con desenfoque y animación escalonada de los enlaces.

## Archivos modificados
- `index.html`

## Comportamiento
| Dispositivo | Resultado |
|---|---|
| Móvil (< 640px) | Enlaces ocultos, botón hamburguesa visible, menú de pantalla completa estilo Apple |
| Escritorio (≥ 640px) | Navbar idéntica a la versión anterior (enlaces inline) |

## Cambios realizados

### 1. Navbar (`<header>`)
- `id="site-header"` en el header e `id="navbar-inner"` en el contenedor interno (para cambiar su aspecto cuando el menú está abierto).
- El logo ahora es un enlace a `#inicio` con clase `nav-brand`.
- Contenedor de enlaces: `hidden sm:flex` → oculto en móvil, visible en escritorio.
- Nuevo botón `#menu-toggle` (`sm:hidden`) con dos `<span class="menu-line">` que se convierten en una **X** animada al abrir.

### 2. Menú de pantalla completa (`<nav id="mobile-menu">`)
- Fondo oscuro translúcido `rgba(22,22,23,.9)` + `backdrop-filter: blur(20px)` (como Apple).
- Enlaces grandes (`28px`, semibold, color `#f5f5f7`): Inicio, Solución, Beneficios, Experiencia.
- Enlace secundario "Prueba gratis" → `/demo`.
- Animación escalonada: cada enlace aparece con fade + deslizamiento y retardos de 0.15s a 0.42s.
- `z-index: 40` (debajo del header `z-50`) para que el logo y el botón X sigan visibles.
- Con el menú abierto la navbar se vuelve transparente y el logo cambia a color claro.

### 3. JavaScript (dentro del `DOMContentLoaded` existente)
- Toggle de la clase `menu-open` en `<body>` al pulsar el botón.
- Cierra el menú al: tocar un enlace, pulsar `Escape`, o redimensionar a ≥ 640px.
- Actualiza `aria-expanded` y `aria-label` ("Abrir menú" / "Cerrar menú").
- `body.menu-open { overflow: hidden }` bloquea el scroll de fondo.

## Cómo probar
1. Abrir `index.html` → DevTools (F12) → modo responsive → iPhone.
2. Verificar que solo se ven logo + hamburguesa.
3. Tocar la hamburguesa: fondo oscuro con blur, enlaces aparecen escalonados, icono se convierte en X.
4. Tocar un enlace: el menú se cierra y hace scroll suave a la sección.
5. Volver a tamaño escritorio: navbar con enlaces inline como siempre.
