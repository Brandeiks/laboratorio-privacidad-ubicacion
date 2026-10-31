# Consentimiento informado

Texto que se entrega (o se lee) a cada participante **antes** de enviarle el enlace. La página repite un resumen en el paso 01.

---

## Laboratorio de privacidad: qué ubicación puede revelar una visita web

**Responsable:** Brandon (estudiante de ciberseguridad, UPC).
**Finalidad:** ejercicio académico para comparar la ubicación estimada por IP con la ubicación que el navegador comparte cuando la persona da permiso.

### Qué se te pedirá

1. Abrir un enlace a una página web.
2. Pulsar un botón para estimar tu ubicación por IP. Esto consulta un servicio externo (ipapi.co o ipwho.is), que recibe tu IP.
3. Si quieres, pulsar «Compartir mi ubicación para la demostración». Tu navegador te pedirá permiso. Puedes aceptarlo o rechazarlo.

### Qué datos se tratan

| Dato | ¿Se muestra? | ¿Se guarda? |
|---|---|---|
| IP pública | Sí, solo a ti | No |
| País, región y ciudad estimados por IP | Sí | Solo si pulsas «Guardar», en tu navegador |
| Latitud y longitud del navegador | Sí | Solo si pulsas «Guardar», redondeadas a ~110 m por defecto |
| Margen de precisión (metros) | Sí | Solo si pulsas «Guardar» |
| Tipo de dispositivo y red (los eliges tú) | — | Solo si pulsas «Guardar» |
| Proveedor de internet, user agent | El proveedor se muestra | No |

### Dónde quedan los datos

- En **tu propio navegador** (`localStorage`). La página no tiene servidor y no envía tus coordenadas a nadie.
- Si decides compartir tus resultados con el responsable, lo haces tú, exportando el CSV o JSON y enviándolo por el medio acordado.

### Tus derechos

- Participar es voluntario. Puedes retirarte cuando quieras.
- Puedes rechazar el permiso de ubicación: también es un resultado válido.
- Puedes borrar tus datos con el botón «Borrar todo» de la página.
- Si enviaste tus resultados al responsable, puedes pedir que se eliminen.

### Marco legal de referencia

Ley N.º 29733, Ley de Protección de Datos Personales (Perú), y su reglamento. Los datos de ubicación precisa pueden identificar a una persona, por eso se minimizan y no se publican.

---

**Confirmación:** al marcar la casilla del paso 01 declaras que leíste este aviso y aceptas participar.
