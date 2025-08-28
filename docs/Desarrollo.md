# Desarrollo
**Título:** Formulario de Contacto Accesible con Confirmación  

## **Descripción**

Implementar un **formulario de contacto accesible** en `contacto.html` con campos Nombre, Email y Mensaje, validaciones en cliente, integración con EmailJS y redirección a `gracias.html`.  
Debe cumplir con estándares de accesibilidad (WCAG 2.1, WAI-ARIA) y buenas prácticas de seguridad básicas contra spam.

## Requisitos

### 1 Requisitos funcionales
- Formulario en `contacto.html` con campos Nombre, Email, Mensaje (obligatorios).  
- Validación de Email y longitud mínima de Mensaje (≥20 caracteres).  
- Campo honeypot oculto para prevenir spam.  
- Redirección a `gracias.html` tras envío exitoso.  
- Feedback accesible en caso de error mediante `aria-live`.

### 2 Requisitos no funcionales
- Script `contacto.js` ≤ 10 KB.  
- Carga diferida (`defer`) para no bloquear renderizado.  
- Navegación por teclado completa; foco visible en todos los estados.  
- Compatibilidad con navegadores modernos (Chrome, Firefox, Edge).  

### 3 Dependencias
- Cuenta de EmailJS con `PUBLIC_KEY`, `SERVICE_ID` y `TEMPLATE_ID`.  
- CDN de EmailJS (`jsdelivr`).  
- Estilos existentes en `style.css`.

## Diseño Técnico

### 1 Arquitectura
- HTML (formulario + contenedor de alertas con `aria-live`).  
- JS (`contacto.js`) para validación, anti-spam y envío.  
- EmailJS SDK para integración.  
- Página `gracias.html` como destino de confirmación.

### 2 Componentes afectados
- `contacto.html`  
- `gracias.html` (nuevo)  
- `js/contacto.js` (nuevo)  
- `css/style.css` (ajustes de estados)  

### 3 Diagramas
Secuencia simplificada:
```
Usuario → contacto.html → contacto.js → EmailJS → respuesta → gracias.html
```

### Pseudocódigo o lógica de alto nivel
```js
onDOMContentLoaded(() => {
  emailjs.init(PUBLIC_KEY);
  const form = q('#contactoForm');
  const hp = q('.hp');
  const submit = form.querySelector('button');
  lockFor(3s, submit);

  form.onsubmit = async (e) => {
    e.preventDefault();
    if (hp.value) return okGeneric();
    const data = readForm(form);
    const errs = validate(data);
    if (errs.length) return showErrors(errs);
    try {
      await emailjs.send(SERVICE_ID, TEMPLATE_ID, data);
      location.href = '/gracias.html';
    } catch {
      announce('No pudimos enviar tu mensaje, intentá nuevamente.');
    }
  };
});
```

## Implementación

### 1 Lenguaje de programación
- JavaScript vanilla (frontend).  

### 2 Frameworks o librerías
- EmailJS Browser SDK.  

### 3 Patrones de diseño
- Módulo único `contacto.js` desacoplado.  
- BEM en CSS para estados de error/validación.  

### 4 Consideraciones de rendimiento
- Script optimizado ≤ 10 KB.  
- Carga con `defer`.  

### 5 Manejo de errores
- Feedback accesible en `aria-live`.  
- Redirección solo en éxito.  

## Base de Datos

### 1 Cambios en el esquema
- No aplica.  

### 2 Consultas SQL
- No aplica.  

### 3 Migración de datos
- No aplica.  

## API

### 1 Endpoints
- No aplica (uso de EmailJS SDK).  

### 2 Autenticación y autorización
- Clave pública EmailJS restringida a dominio.  

### 3 Formato de datos
- JSON enviado a EmailJS.  

## Interfaz de Usuario

### 1 Mockups o wireframes
- Formulario con tres campos + botón enviar + bloque de mensajes.  

### 2 Comportamiento de la UI
- Botón enviar deshabilitado durante 3 s tras carga.  
- Validaciones en vivo con estados de error/validación.  
- Redirección a `gracias.html` en éxito.  

### 3 Consideraciones de accesibilidad
- Labels asociados por `for/id`.  
- `aria-live` para mensajes de error/confirmación.  
- Foco visible en inputs y botón.  

## Pruebas

### 1 Pruebas unitarias
- Validación de Email.  
- Longitud mínima de Mensaje.  
- Detección de honeypot.  

### 2 Pruebas de integración
- Envío correcto con EmailJS.  
- Manejo de error en red.  

### 3 Pruebas de aceptación
- Flujo completo contacto.html → gracias.html.  
- Accesibilidad (tab, lector de pantalla).  

## Despliegue

### 1 Entorno de despliegue
- Hosting estático (ej. GitHub Pages, Netlify, Vercel).  

### 2 Configuración
- Variables de EmailJS (`PUBLIC_KEY`, `SERVICE_ID`, `TEMPLATE_ID`).  

### 3 Scripts de despliegue
- Subida simple de archivos estáticos.  

### 4 Enlace a Merge Request
- *Pendiente al crear MR.*  

## Documentación

### 1 Documentación técnica
- Actualizar manual técnico con instrucciones de configuración EmailJS.  

### 2 Documentación de usuario
- Instrucciones simples en `contacto.html`: qué campos completar.  

## Consideraciones de Seguridad
- Honeypot + delay anti-spam.  
- Restricción de claves EmailJS por dominio.  
- Comunicación HTTPS con servicio externo.  
