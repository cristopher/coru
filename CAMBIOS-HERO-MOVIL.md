# Cambios: Hero a ancho completo en móvil

## Objetivo
Que el hero ocupe **todo el ancho de la pantalla** cuando se ve desde un teléfono (iPhone), sin tocar el diseño actual de escritorio.

## Archivos modificados
- `index.html`

## Cambios realizados

### 1. Regla CSS con media query (`<style>` en el `<head>`)
Nueva regla que solo se aplica en pantallas **menores a 640px**:

```css
@media (max-width: 639px) {
  #inicio {
    position: relative;
    left: 50%;
    right: 50%;
    margin-left: -50vw;
    margin-right: -50vw;
    width: 100vw;
    padding-top: 0;
    margin-top: -1.25rem; /* Compensa el py-5 del contenedor padre */
  }
}
```

- Usa la misma técnica de "full-bleed" que ya usa la sección "El costo oculto" (`-ml-[50vw]` + `w-screen`).
- Elimina el espacio superior para que el hero quede pegado al navbar.
- El contenedor padre ya tiene `overflow-x-hidden`, por lo que no aparece scroll horizontal.

### 2. Tarjeta del hero (esquinas y borde)
Antes:
```
rounded-3xl border border-white/20
```
Ahora:
```
rounded-none sm:rounded-3xl border-0 sm:border sm:border-white/20
```

- En móvil: sin esquinas redondeadas ni borde (look full-bleed).
- En escritorio (≥ 640px): idéntico a antes.

## Comportamiento por dispositivo
| Dispositivo | Resultado |
|---|---|
| iPhone / móvil (< 640px) | Hero de borde a borde, sin márgenes laterales, sin redondeo, pegado al navbar |
| Tablet / PC (≥ 640px) | Exactamente igual que la versión actual |

## Cómo probar
1. Abrir `index.html` en el navegador.
2. Abrir DevTools (F12) → modo responsive → seleccionar un iPhone.
3. Verificar que el hero llega hasta los bordes laterales.
4. Volver a tamaño escritorio y verificar que todo sigue igual.
