# Assets Locales Descargados

He descargado y configurado todos los recursos externos para que funcionen localmente:

## Archivos Descargados:

### 📁 CSS/
- `plus-jakarta-sans.css` - CSS de la fuente Plus Jakarta Sans (400, 500, 700)
- `material-symbols-outlined-local.css` - CSS simplificado para iconos Material Symbols
- `tailwind.js` - Tailwind CSS completo (versión 3.4.1)

### 📁 fonts/
- `plus-jakarta-sans-regular.ttf` - Fuente regular (400)
- `plus-jakarta-sans-medium.ttf` - Fuente medium (500) 
- `plus-jakarta-sans-bold.ttf` - Fuente bold (700)
- `material-symbols-outlined-regular.ttf` - Iconos Material Symbols

## Archivos HTML Modificados:

### Archivo Principal:
- `index.html` - Modificado para usar archivos locales en lugar de CDN

### Backup:
- `index-local.html` - Versión completa con todos los cambios

## Cambios Realizados:

1. **Fuentes Google** → Archivos locales:
   - Plus Jakarta Sans descargada en 3 pesos
   - Material Symbols Outlined descargada (solo peso 400)
   - Archivos CSS modificados para apuntar a archivos locales

2. **Tailwind CSS** → Archivo local:
   - Descargada versión completa desde CDN
   - Configuración mantenida sin plugins que requieran npm

## Para Usar:

1. Abrir `index.html` en cualquier navegador
2. La página funcionará completamente offline
3. No se requieren conexiones externas para fuentes o CSS

## Notas:
- Las imágenes siguen siendo externas (Google Photos)
- Los plugins de Tailwind (@tailwindcss/forms, @tailwindcss/container-queries) fueron removidos por requerir npm
- La funcionalidad básica del sitio se mantiene intacta