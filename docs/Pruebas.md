# Pruebas
**Título:** Formulario de Contacto Accesible con Confirmación  

## Información General

### 1 Objetivo
Validar que el **formulario de contacto** en `contacto.html` funcione correctamente, cumpla criterios de accesibilidad, integre EmailJS y redirija a `gracias.html` en envíos exitosos.

### 2 Alcance
- Validación de campos (**Nombre**, **Email**, **Mensaje**).
- Comportamiento de error y confirmación (región `aria-live`).
- Anti‑spam (honeypot + delay de 3 s).
- Redirección a `gracias.html`.
- Compatibilidad en navegadores modernos (Chrome/Firefox/Edge).

### 3 Fuera del alcance
- Integración con CRM o guardado en BD.
- Captcha externo (reCAPTCHA).
- Telemetría/analítica.

### 4 Entorno de pruebas
- Sitio estático local/hosting de pruebas.
- Navegadores: Chrome 126+, Firefox 128+, Edge 126+.
- Conectividad a **EmailJS** con `PUBLIC_KEY`, `SERVICE_ID`, `TEMPLATE_ID` de prueba.

## Recursos

### 1 Equipo de pruebas
- Responsable QA: Sergio Aguilar
- Soporte técnico: Dev Front/Contenido

### 2 Herramientas
- Navegadores de escritorio.
- Extensión Lighthouse (Accesibilidad).
- Herramientas de devtools (Network/Console).

### 3 Datos de prueba
- Nombre: `Ana Pérez`
- Email válido: `ana.perez@example.com`
- Email inválido: `ana@perez` / `ana@perez.`
- Mensaje válido: `Quiero un presupuesto para un sitio web corporativo…` (≥ 20 chars)
- Mensaje corto: `Hola`

## Tipos de Pruebas

### 1 Pruebas funcionales
- **PF-01 Envío válido**  
  - **Dado** que estoy en `contacto.html`  
  - **Cuando** completo Nombre, Email válido y Mensaje ≥ 20 caracteres y envío  
  - **Entonces** se envía con EmailJS y soy redirigido a `gracias.html`  

- **PF-02 Email inválido**  
  - Email sin TLD o con formato incorrecto → bloquea envío y muestra error accesible.

- **PF-03 Campos requeridos**  
  - Enviar con campos vacíos → muestra errores y no envía.

- **PF-04 Mensaje corto**  
  - Mensaje < 20 caracteres → muestra error y no envía.

- **PF-05 Honeypot**  
  - Completar campo oculto → no envía; muestra confirmación/ok genérico sin error visible.

- **PF-06 Delay de botón**  
  - Intentar enviar antes de 3 s → botón deshabilitado; tras 3 s, habilitado.

- **PF-07 Manejo de error EmailJS**  
  - Simular fallo de red/API → no redirige; muestra mensaje accesible en `aria-live`.

### 2 Pruebas de integración
- **PI-01 Integración EmailJS**: confirmar que `emailjs.send` recibe los campos correctos y retorna éxito (mock o credencial de prueba).

### 3 Pruebas de rendimiento
- **PR-01 Peso JS**: `contacto.js` ≤ 10 KB (inspección en Network).  
- **PR-02 Carga no bloqueante**: script con `defer` y sin CLS por mensajes.

### 4 Pruebas de seguridad (básicas)
- **PS-01 Honeypot** operativo (no rompe accesibilidad).  
- **PS-02 Sin datos extraños**: sanitización básica (no inyecta HTML).  
- **PS-03 Clave pública**: no aparecen credenciales privadas en el código/Network.

### 5 Pruebas de accesibilidad
- **PA-01 Labels y `for/id`**: cada input tiene su label asociado.  
- **PA-02 Navegación por teclado**: orden lógico, sin trampas de foco.  
- **PA-03 Foco visible**: en inputs y botón enviar.  
- **PA-04 `aria-live`**: mensajes de error/estado se anuncian al actualizarse.  
- **PA-05 Contraste**: estilos de error cumplen contraste mínimo (verificación visual o con herramienta).  
- **PA-06 Lighthouse A11Y ≥ 90** en `contacto.html`.

## Matriz de Casos (resumen)

| ID | Nombre | Tipo | Precondición | Pasos clave | Resultado esperado |
|----|--------|------|--------------|-------------|--------------------|
| PF-01 | Envío válido | Funcional | Página cargada | Completar datos válidos y enviar | Redirige a `gracias.html` |
| PF-02 | Email inválido | Funcional | Página cargada | Email `ana@perez` | Error accesible; no envía |
| PF-03 | Requeridos | Funcional | Página cargada | Enviar con campos vacíos | Errores accesibles; no envía |
| PF-04 | Mensaje corto | Funcional | Página cargada | Mensaje `<20` | Error accesible; no envía |
| PF-05 | Honeypot | Seguridad | Página cargada | Completar campo oculto | No envía; ok genérico |
| PF-06 | Delay botón | Funcional | Página recién cargada | Enviar antes de 3 s | Botón deshabilitado |
| PF-07 | Fallo EmailJS | Integración | API caída/mock | Forzar error | Mensaje en `aria-live`; no redirige |
| PA-06 | Lighthouse A11Y | Accesibilidad | Página cargada | Ejecutar Lighthouse | Score ≥ 90 |

## Criterios de Aceptación (DoR/DoD)

**Entrada (DoR):**  
- HU y Análisis aprobados.  
- Credenciales de prueba para EmailJS configuradas.  
- `contacto.html` con formulario y `aria-live` implementados.  

**Salida (DoD):**  
- Todos los casos **PF/PI/PR/PS/PA** aprobados.  
- 0 errores en consola durante PF‑01.  
- Lighthouse A11Y ≥ 90.  
- Redirección a `gracias.html` en éxito.  
- Documentación de pruebas adjunta (evidencias).  

## Gestión de Riesgos de Prueba
- Intermitencia en EmailJS → usar mock o credencial de sandbox.  
- Bloqueo por CSP en entorno → validar whitelist a `cdn.jsdelivr.net`.  
- Falsos positivos honeypot → validar que usuarios reales no lo completen (oculto y fuera de tab).

## Evidencias Esperadas
- Capturas de: errores accesibles, envío exitoso, `gracias.html`, Lighthouse.  
- Logs de Network mostrando llamada a `emailjs.send` en éxito/fallo.

## Control de Cambios
| Versión | Fecha | Autor | Descripción |
|--------|-------|-------|-------------|
| 1.0 | 27/08/2025 | Sergio Aguilar | Versión inicial |
