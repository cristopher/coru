# Integración del Formulario de Contacto

- El formulario de `/demo/index.html` envía un `POST` JSON a `https://costos.minck.cl/contacto/enviar`.
- Los campos del formulario se transforman al contrato del endpoint:
  - `nombre` -> `nombre_completo`
  - `empresa` -> `constructora`
  - `email` -> `correo_electronico`
  - `telefono` -> `telefono`
- Se agregó estado de carga, confirmación de envío exitoso y mensaje de error con posibilidad de reintentar.
