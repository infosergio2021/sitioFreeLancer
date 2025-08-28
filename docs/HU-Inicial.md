# Historia de Usuario

ID: HU-FREE-001  
Estado: Sin empezar  
Título: HU – Formulario de Contacto Accesible con Confirmación

## Objetivo

Implementar un **formulario de contacto accesible y funcional** en `contacto.html` que permita enviar consultas **sin abrir el cliente de correo**, mostrando confirmación clara al usuario.

## Descripción

Actualmente el sitio es estático y el enlace de contacto no realiza un envío real.  
Se requiere un formulario con **validación en cliente**, **mensajes accesibles**, y **confirmación de envío** mediante una página `gracias.html`.  
El envío se resolverá **sin backend propio** usando un servicio tipo EmailJS.

## Entorno

- Proyecto: `sitioFreeLancer-master` (HTML/CSS/JS)  
- Páginas relevantes: `contacto.html`, `gracias.html` (nueva)  
- Navegadores objetivo: Chrome/Firefox/Edge modernos  
- Restricciones: sitio estático, sin servidor propio

## Capturas de pantalla/videos

[](https://www.notion.so)  
[https://www.notion.so](https://www.notion.so)

## Detalles

| **Componente/Función** | **Acción** | **Funcionalidad** | **Resultado esperado** |
|-------------------------|------------|-------------------|-------------------------|
| contacto.html | Crear formulario con Nombre, Email, Mensaje | Validación + envío vía EmailJS | Mensaje enviado / Errores accesibles |
| gracias.html | Nueva página | Mostrar confirmación del envío | Usuario recibe feedback claro |
| contacto.js | Script asociado | Validación de campos, honeypot, integración con EmailJS | Datos enviados a destino |
| style.css | Ajustes de estilos | Estados de error, foco visible | Accesibilidad y consistencia visual |

## Comportamiento esperado

- El usuario accede a `contacto.html` y visualiza un formulario con campos **Nombre**, **Email** y **Mensaje**, todos etiquetados con `<label>`.
- Si intenta enviar con datos inválidos o incompletos, se muestran **mensajes de error descriptivos** (accesibles vía `aria-live`), y el envío se bloquea.
- Si completa los campos correctamente y envía, se procesa la solicitud y el usuario es **redirigido a `gracias.html`** con un mensaje de confirmación.
- Se implementa un **honeypot** (campo oculto) para mitigar spam.
- El formulario es **navegable con teclado** y el foco es visible.
- El script del formulario se carga con `defer` y no bloquea el render.

## Criterios de aceptación

- [ ] El formulario en `contacto.html` incluye **Nombre**, **Email**, **Mensaje**, con `label` asociado y validaciones.  
- [ ] Validación de **Email** con patrón adecuado; mensajes de error claros y accesibles (`aria-live`).  
- [ ] **Mensaje** requiere al menos **20 caracteres**.  
- [ ] Implementado **honeypot** para evitar spam.  
- [ ] En **éxito**, redirige a `/gracias.html`.  
- [ ] Navegación por teclado completa; foco visible.  
- [ ] No hay errores en consola durante el flujo válido.  
- [ ] El script de envío se carga con `defer` y pesa ≤ 10 KB.  

## Notas adicionales

- Envío sin backend propio sugerido con **EmailJS**.  
- Fuera de alcance: integración con CRM, reCAPTCHA, almacenamiento en base de datos propia.  
- Posible evolución: agregar métricas de envío y bloqueo por tiempo para reducir spam.
