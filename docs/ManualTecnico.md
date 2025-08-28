# Manual Técnico
**Título:** Formulario de Contacto Accesible con Confirmación

## Introducción

### 1 Propósito del documento
Este manual describe la implementación técnica del formulario de contacto en `contacto.html`, su integración con **EmailJS** y las consideraciones de accesibilidad, seguridad y despliegue. Está dirigido a desarrolladores que mantendrán el sitio estático.

### 2 Alcance del sistema
El sistema es un sitio estático (HTML/CSS/JS).  
El formulario permite a un visitante enviar un mensaje que se entrega vía EmailJS, sin necesidad de backend propio.  

### 3 Definiciones, acrónimos y abreviaturas
- **EmailJS**: Servicio para enviar emails desde el navegador.  
- **WCAG 2.1**: Estándar de accesibilidad web.  
- **ARIA live region**: Área que anuncia cambios dinámicos a lectores de pantalla.  
- **Honeypot**: Campo oculto usado como trampa anti-spam.  

## Descripción general del sistema

### 1 Perspectiva del producto
El formulario se integra dentro de `contacto.html` y agrega la página `gracias.html`. Se conecta con el servicio EmailJS.  

### 2 Funciones del producto
- Mostrar un formulario accesible.  
- Validar datos antes del envío.  
- Evitar spam (honeypot + delay de 3 s).  
- Redirigir a `gracias.html` en éxito.  

### 3 Características de los usuarios
- Visitantes del sitio que desean enviar un mensaje.  
- Desarrolladores encargados de mantenimiento.  

### 4 Limitaciones
- No existe backend propio.  
- El envío depende de la disponibilidad de EmailJS.  

## Arquitectura del sistema

### 1 Diagrama de arquitectura
Usuario → contacto.html → contacto.js → EmailJS → respuesta → gracias.html

### 2 Componentes del sistema
- `contacto.html`: formulario accesible con campos obligatorios.  
- `contacto.js`: validación, integración EmailJS, honeypot, mensajes accesibles.  
- `gracias.html`: confirmación de envío.  
- `style.css`: estilos de estados de error y validación.  

### 3 Interfaces del sistema
- Navegador (HTML + JS).  
- EmailJS API.  

## Diseño detallado

### 1 contacto.html
- Propósito: formulario principal.  
- Diseño: inputs con `<label>` y `aria-live`.  
- Dependencias: `contacto.js`.  

### 2 contacto.js
- Propósito: validación y envío.  
- Diseño interno: inicialización de EmailJS, validación, feedback accesible.  
- Algoritmos clave: validación de email, longitud mínima de mensaje, honeypot.  

### 3 gracias.html
- Propósito: confirmar el envío.  
- Diseño: mensaje con link de retorno a inicio.  

## Base de datos

### 1 Modelo de datos
No aplica (no se persiste información).  

### 2 Diccionario de datos
No aplica.  

### 3 Relaciones y constraints
No aplica.  

## APIs y servicios web

### 1 APIs internas
No aplica.  

### 2 APIs externas
- **EmailJS**: `emailjs.send(SERVICE_ID, TEMPLATE_ID, data)`.  

### 3 Autenticación y seguridad
- Uso de `PUBLIC_KEY` limitado a dominio y plantilla en EmailJS.  

## Seguridad

### 1 Autenticación y autorización
No aplica (flujo público).  

### 2 Encriptación
Comunicación HTTPS con EmailJS.  

### 3 Auditoría y logging
- Console logs básicos para éxito/fallo.  

## Rendimiento y escalabilidad

### 1 Métricas de rendimiento
- `contacto.js` ≤ 10 KB.  
- Lighthouse A11Y ≥ 90.  

### 2 Estrategias de caché
- Uso de caching estándar de navegador/CDN.  

### 3 Balanceo de carga
- No aplica (sitio estático).  

## Despliegue

### 1 Requisitos de infraestructura
- Hosting estático (ej. GitHub Pages, Netlify, Vercel).  

### 2 Proceso de instalación
- Subir `contacto.html`, `gracias.html`, `css/style.css`, `js/contacto.js`.  

### 3 Configuración
- Ingresar claves de EmailJS (`PUBLIC_KEY`, `SERVICE_ID`, `TEMPLATE_ID`) en el código.  

## Mantenimiento y soporte

### 1 Monitoreo
- Revisar funcionamiento del formulario manualmente.  
- Posible integración futura con analítica.  

### 2 Backups y recuperación
- Copia de seguridad de archivos estáticos y claves de EmailJS.  

### 3 Actualizaciones y parches
- Verificar cambios de versión en EmailJS SDK.  

## Control de Cambios

| **Versión** | **Fecha**   | **Autor**         | **Descripción** |
|-------------|-------------|-------------------|-----------------|
| 1.0         | 27/08/2025  | Sergio Aguilar    | Versión inicial |
