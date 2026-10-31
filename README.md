# Laboratorio de privacidad: qué ubicación puede revelar una visita web

> Receta práctica: cómo funciona, qué pasos seguir y qué hace falta para llevarlo a cabo.
> Uso académico y solo con participantes que aceptaron el ejercicio.

---

## Cómo usarlo

**En local** (desde esta carpeta):

```bash
python -m http.server 5500
```

Luego abre `http://localhost:5500`. La geolocalización solo funciona en `localhost` o HTTPS, por eso no basta con abrir `index.html` con doble clic.

**En GitHub Pages:** sube la carpeta a un repositorio, activa Pages (Settings → Pages → rama `main`, carpeta raíz) y comparte el enlace `https://<usuario>.github.io/<repositorio>/` con los participantes.

## Estructura

```
laboratorio-privacidad-ubicacion/
├── index.html              # La página: aviso, pasos 01–06
├── assets/
│   ├── styles.css          # Estética del laboratorio
│   └── app.js              # Lógica: GeoIP, geolocalización, comparación, guardado
└── docs/
    ├── consentimiento.md   # Texto para los participantes
    └── resultados.md       # Plantilla para el informe
```

## Qué hace la página

| Paso | Qué ocurre |
|---|---|
| 01 · Antes de empezar | Aviso de qué se pide, para qué y cómo se borra. Los botones no se activan hasta marcar la casilla |
| 02 · Estimación por IP | Consulta ipapi.co (o ipwho.is si falla) y muestra país, región, ciudad y coordenadas aproximadas |
| 03 · Ubicación del navegador | Llama a `navigator.geolocation`, muestra latitud, longitud y precisión, o el motivo del rechazo |
| 04 · Comparación | Distancia entre ambos métodos y cuántas veces se desvía la IP respecto al margen del navegador |
| 05 · Guardar y borrar | Guarda el intento en `localStorage` (coordenadas redondeadas por defecto), exporta CSV/JSON y borra todo |
| 06 · Qué sale a la red | Tabla de transparencia: cada destino externo y qué recibe |

**Decisiones de seguridad:** no hay backend; los datos externos se pintan con `textContent` (nunca `innerHTML`); no se guardan IP, proveedor ni user agent; `referrer` desactivado; nada se pide al cargar la página.

---

## Ingredientes (lo necesario)

**Conocimiento previo**

- HTML y JavaScript básico.
- Idea general de qué es una IP pública.
- Nociones de privacidad y consentimiento informado.

**Herramientas**

- Un editor de texto (VS Code, por ejemplo).
- Un navegador moderno (Brave o Chrome) con permisos de ubicación.
- Git y cuenta de GitHub, para subir el proyecto.
- Un servidor local sencillo (la extensión Live Server, o `python -m http.server`) para probar en `localhost`.

**Materiales del proyecto**

- Un texto de consentimiento claro para los participantes.
- Dos o tres dispositivos de prueba (PC, móvil y una red distinta, si es posible).
- Un lugar para anotar resultados (una hoja de cálculo o `docs/resultados.md`).

**Recursos externos**

- Un servicio de geolocalización por IP para la estimación de país o ciudad. Revisar sus términos de uso y límites antes de usarlo.
- MDN: Geolocation API y contextos seguros.

---

## Preparación

1. **Define la pregunta.** Ejemplo: *¿Qué ubicación puede estimar una web sin permiso y qué cambia cuando el usuario acepta?*
2. **Redacta el consentimiento.** Qué se pide, para qué, si se guarda, cuánto tiempo y cómo se borra. El participante debe leerlo antes del botón.
3. **Crea el repositorio.** Carpeta `laboratorio-privacidad-ubicacion` con `README.md` y, más adelante, `index.html`.
4. **Decide el almacenamiento.** Recomendado: nada sale del navegador. Los datos quedan en `localStorage` y hay un botón para borrarlos.

---

## Flujo de funcionamiento

```
[Participante abre el enlace]
            │
            ▼
[La página muestra el aviso: qué se pide, para qué, si se guarda]
            │
            ├── No acepta ──► La página no obtiene coordenadas. Fin.
            │
            ▼
[Pulsa «Compartir mi ubicación para la demostración»]
            │
            ▼
[El navegador muestra su propio aviso de permiso]
            │
            ├── Rechaza ──► Se registra el rechazo (sin datos personales). Fin.
            │
            ▼
[Acepta]
            │
            ▼
[Se muestran latitud, longitud y precisión en metros]
            │
            ▼
[Opcional: se compara con la estimación por IP]
            │
            ▼
[Se guarda solo lo autorizado, con botón para borrarlo]
```

---

## Pasos de la receta

**Paso 1: Página de aviso.** Muestra el texto de consentimiento antes de cualquier petición. Sin este paso, no hay demostración.

**Paso 2: Botón explícito.** Una sola acción que dispara la petición de ubicación. Nada se pide al cargar la página.

**Paso 3: Petición al navegador.** Se llama a `navigator.geolocation` y el navegador pide permiso. Si el participante rechaza, la página recibe un error y no obtiene coordenadas.

**Paso 4: Mostrar resultados.** Se muestran latitud, longitud y precisión en metros. Explicar que la precisión es un radio aproximado, no una posición exacta.

**Paso 5: Estimación por IP (opcional).** Se consulta un servicio de geolocalización por IP y se muestra país o ciudad. Se compara con la ubicación autorizada.

**Paso 6: Guardado y borrado.** Si el participante acepta guardar, se almacena en su navegador. Debe haber un botón para borrar todo. No se guardan IP, user agent ni identificadores.

**Paso 7: Análisis.** Anotar distancias entre IP y coordenadas autorizadas, precisión por dispositivo y tiempo de respuesta. Escribir conclusiones en `docs/resultados.md`.

---

## Resultado esperado

- Un enlace de demostración que explica qué pide antes de pedirlo.
- Una comparación real entre estimación por IP y ubicación autorizada.
- Evidencia de que el permiso del navegador y el consentimiento cambian lo que la web puede saber.
- Un informe corto con límites, errores y recomendaciones de privacidad.

---

## Precauciones (no saltarse)

- **Consentimiento antes que todo.** Sin aceptación explícita, no hay petición.
- **Nada de terceros.** No usar enlaces ni datos de personas que no participaron.
- **Sin datos reales en el repositorio.** No subir coordenadas, IP ni capturas de participantes.
- **HTTPS o `localhost`.** La geolocalización del navegador no funciona en contextos no seguros.
- **Ley aplicable.** En Perú, revisar la Ley N.º 29733 (Protección de Datos Personales) antes de recolectar datos reales.
- **Límites de precisión.** La IP puede estar desactualizada y el GPS puede fallar en interiores. Decirlo en el informe.

---

## Errores comunes

| Problema | Causa probable | Solución |
|---|---|---|
| El navegador no pide permiso | La página no está en HTTPS ni en `localhost` | Probar en `localhost` o publicar en GitHub Pages |
| Precisión de miles de metros | Solo hay Wi-Fi o IP, sin GPS | Probar en el móvil y anotarlo como variable |
| La IP da otra ciudad | Base de datos de IP desactualizada | Documentarlo como limitación |
| El participante no entiende el aviso | Texto demasiado técnico | Reescribir en lenguaje simple |

---

## Lista de tareas

- [x] Redactar el texto de consentimiento (`docs/consentimiento.md`)
- [x] Elegir el servicio de geolocalización por IP (ipapi.co, con ipwho.is de respaldo)
- [ ] Revisar los términos de uso de ambos servicios
- [x] Crear `index.html` con aviso, botón y resultados
- [ ] Probar en `localhost` con permiso aceptado y rechazado
- [x] Añadir el botón para borrar datos
- [ ] Verificar en DevTools (pestaña Network) que las coordenadas no salen a la red
- [ ] Probar en al menos dos dispositivos
- [ ] Escribir `docs/resultados.md`
- [ ] Subir a GitHub y activar GitHub Pages

---

## Referencias

- MDN: [Geolocation API](https://developer.mozilla.org/es/docs/Web/API/Geolocation_API)
- MDN: [Contextos seguros](https://developer.mozilla.org/es/docs/Web/Security/Secure_Contexts)
- Ley N.º 29733, Ley de Protección de Datos Personales (Perú)
