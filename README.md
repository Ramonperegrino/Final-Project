# Página accesible: Nissan vs Toyota

Archivos incluidos:

- `index.html` — Página estática accesible con regiones semánticas, imágenes (SVG inline), enlaces, tabla y formulario corto.
- `styles.css` — Estilos básicos y responsivos.
 - `about.html` — Página "Acerca" con contexto y contacto.
 - `survey.html` — Página dedicada a la encuesta con validación ligera.

Cómo abrirlo:

1. Abre `index.html` en tu navegador (doble clic o "Abrir con").
2. Usa Tab para navegar y prueba la "Saltar al contenido" (Skip link).

Qué cubrí para accesibilidad (y cambios recientes):

- Estructura semántica: `header`, `nav`, `main`, `footer`, `section`.
- Texto alternativo en imágenes.
- Tabla con `caption`, `thead`, `th scope` y `tbody` (se eliminó el atributo `summary` obsoleto).
- Formulario con `fieldset`, `legend`, y etiquetas `label` enlazadas con `for`.
- Skip link visible al recibir foco.
- Mejoras añadidas ahora:
	- Contraste del color de acento ajustado para mejorar legibilidad en enlaces y botones.
	- Estilos de foco más visibles y consistentes para enlaces, botones e inputs.
	- Validación de formulario reforzada en el cliente: mensajes visibles junto a los campos (marca y correo), enfoque en el primer error y confirmación visible al enviar.
	- Mensajes de error y estados visuales (clase `.error`) para hacer más evidente la corrección requerida.

Si quieres que añada almacenamiento local de votos, una versión en inglés o un informe automatizado de accesibilidad (Lighthouse), dímelo y lo preparo.

**Requisitos de accesibilidad (encargo)**

- Objetivo principal: Todas las páginas del sitio deben pasar con 0 errores reportados por Silktide para **WCAG 2.2 AA**, tanto en versión de escritorio como móvil.

Comprobaciones adicionales que deben cumplirse o revisarse manualmente:

- **Acceso completo por teclado** — SC 2.1.1 Keyboard (A). Asegúrate de que todos los controles interactivos sean operables con teclado.
- **Orden de foco correcto** — SC 2.4.3 Focus Order (A). El orden del DOM debe coincidir con el orden visual lógico.
- **Foco visible** — SC 2.4.7 Focus Visible (AA). Todos los elementos interactivos deben mostrar un indicador claro de foco.
- **Regiones visuales y no visuales correspondientes** — `header`, `nav`, `main`, `footer` (SC 1.3.6 Identify Purpose — AAA). Usa elementos semánticos para representar las regiones.

Cómo comprobarlo (herramientas y pasos sugeridos)

- Silktide (recomendado por el encargo):
	1. Abre https://www.silktide.com/ o la extensión/servicio que uses para ejecutar análisis.
	2. Introduce la URL local (puedes servir la carpeta con un servidor local) o sube los archivos según permita la herramienta.
	3. Ejecuta el análisis en modo escritorio y en modo móvil. Corrige los problemas reportados hasta obtener 0 errores.

- Alternativa: Lighthouse (incluido en Chrome DevTools o CLI)
	- Abrir DevTools → Lighthouse → seleccionar 'Accessibility' y ejecutar para Desktop y Mobile.
	- CLI (requiere Node):
		```powershell
		npm install -g lighthouse
		lighthouse http://localhost:8000/index.html --preset=desktop --output html --output-path=lh-desktop.html
		lighthouse http://localhost:8000/index.html --preset=mobile --output html --output-path=lh-mobile.html
		```

- Alternativa/Complemento: axe (extensión de navegador o axe-core CLI)
	- Extensión browser: instalar 'axe DevTools' y ejecutar sobre la página.
	- CLI (npm): `npm install -g @axe-core/cli` y usar `axe http://localhost:8000/index.html`.

Recomendaciones de corrección (prioridades comunes)

- Revisar el orden del DOM: asegúrate de que `header`, `nav`, `main`, `footer` aparezcan en el orden visual y que no haya elementos con `tabindex` positivo que cambien el orden.
- Mantener estilos de foco visibles y consistentes (la hoja `styles.css` ya incluye reglas `:focus-visible`).
- Asegurar que todos los controles (enlaces, botones, inputs) sean accesibles desde el teclado y tengan texto visible o atributos `title`/`aria-label` sólo cuando sea estrictamente necesario (evitar añadir nuevos ARIA salvo que sea imprescindible).
- Etiquetado correcto de formularios: `label` asociado a `input` mediante `for`/`id` (ya presentes en el formulario de encuesta).
- Texto alternativo en imágenes significativas (ya aplicado a las fotos añadidas). Para imágenes puramente decorativas, usar `alt=""`.
- Contraste de color: verificar colores del tema (por ejemplo `--accent`) con la herramienta de contraste y ajustar si Silktide lo indica.
- Evitar elementos con `tabindex` mayores a 0 y minimizar el uso de `tabindex="-1"` solo para elementos que deben ser programáticamente enfocables.
- Revisar tablas: `caption`, `thead`, `th scope` y `tbody` ya están presentes en la tabla comparativa.

Flujo recomendado para alcanzar 0 errores en Silktide

1. Ejecutar un análisis en Silktide (escritorio). Anotar errores y warnings.
2. Corregir los errores que sean fácilmente reparables (etiquetas `label`, contrastes, focus, tabindex).
3. Volver a analizar en Silktide y repetir hasta que queden 0 errores.
4. Ejecutar la misma secuencia para la vista móvil.

Si quieres, puedo:
- Preparar un pequeño script para servir los archivos localmente y ejecutar Lighthouse automáticamente.
- Revisar y corregir los problemas que Silktide reporte si me proporcionas el reporte o permiso para ejecutar herramientas locales.

