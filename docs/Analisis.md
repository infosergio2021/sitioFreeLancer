# Análisis Técnico – HU-FREE-001  
**Título:** Formulario de Contacto Accesible con Confirmación  

ID: HU-FREE-001  
Estado: Sin empezar  

## **Propósito**

Definir las decisiones técnicas, alcance y riesgos para implementar un **Formulario de Contacto Accesible con Confirmación** en `contacto.html`, incorporando validación en cliente y redirección a `gracias.html` **sin backend propio**, utilizando un servicio de correo desde el cliente (EmailJS).

## **Contexto y Valor Estratégico**

- El sitio `sitioFreeLancer-master` es **estático** (HTML/CSS/JS). Hoy no existe envío real desde `contacto.html`.  
- El formulario habilita un **canal directo de contacto** sin depender de clientes de correo, mejorando **conversiones** y **experiencia de usuario**.  
- Requisito no funcional clave: **accesibilidad** (WAI-ARIA, navegación por teclado, foco visible).  
- Se prioriza **time-to-market**: uso de EmailJS evita construir y exponer un backend.  

## Arquitectura del Sistema

### 1 Diagrama de Arquitectura


### 2 Descripción de Componentes
- `contacto.html`: formulario accesible.  
- `gracias.html`: confirmación de envío.  
- `contacto.js`: validación, anti-spam, integración EmailJS.  
- `style.css`: estados `.is-error`, `.is-valid`, `.is-loading`.  

## Tecnologías Utilizadas

### 1 Backend
- No aplica (sitio estático sin servidor propio).

### 2 Frontend
- HTML5, CSS3, JavaScript (vanilla).  
- Librería: EmailJS Browser SDK.  

### 3 Otras Tecnologías
- CDN: jsDelivr para EmailJS.  
- BEM como convención CSS.  
- Posible integración futura con pipeline de CI/CD simple.  

## Diseño de Base de Datos

### 1 Modelo de Datos
- No aplica (no se persiste información en BD propia).

### 2 Descripción de Tablas Principales
- No aplica.  

## APIs y Servicios

### 1 APIs Internas
- No aplica.  

### 2 Integraciones Externas
- **EmailJS**  
  - Propósito: enviar correos desde el cliente sin backend.  
  - Método de integración: SDK desde CDN (`emailjs.send`).  

## Seguridad

- Autenticación: clave pública de EmailJS restringida por dominio.  
- Autorización: no aplica (flujo público).  
- Encriptación: comunicación HTTPS con EmailJS.  
- Anti-spam: honeypot + delay de 3s.  
- CSP: verificar que no se bloquee `cdn.jsdelivr.net`.  

## Escalabilidad y Rendimiento

- Script `contacto.js` ≤ 10 KB.  
- Uso de `defer` para no bloquear render.  
- Hosting estático escalable en cualquier CDN.  

## Manejo de Errores y Logging

- Feedback accesible en `aria-live` para errores.  
- `console.info` en éxito/fallo (telemetría opcional).  
- Redirección a `gracias.html` en éxito.  

## Proceso de Despliegue

- Entorno: hosting estático.  
- Pipeline: subida de archivos (`/css`, `/js`, `contacto.html`, `gracias.html`).  
- Rollback: restaurar versión previa de `contacto.html`.  

## Consideraciones de Mantenimiento

- Mantener claves de EmailJS actualizadas.  
- Revisar compatibilidad del SDK con navegadores.  
- Backups no requeridos (no hay BD).  

## Riesgos Técnicos y Mitigaciones

| Riesgo                        | Impacto | Probabilidad | Estrategia de Mitigación |
|-------------------------------|---------|--------------|---------------------------|
| Exposición de clave pública   | Medio   | Media        | Restringir clave por dominio y plantilla |
| Bloqueo por CSP               | Alto    | Baja         | Permitir `cdn.jsdelivr.net` o servir SDK local |
| Falsos positivos de spam      | Bajo    | Media        | Ajustar honeypot y longitud mínima |
| Errores de red al enviar mail | Medio   | Media        | Mensajes claros y posibilidad de reintento |

## Referencias

- [EmailJS Browser SDK](https://www.emailjs.com/docs)  
- [WAI-ARIA Live Regions](https://www.w3.org/TR/wai-aria/#aria-live)  
- [WCAG 2.1](https://www.w3.org/TR/WCAG21/)  

## Glosario

- **EmailJS**: Servicio que permite enviar emails desde el navegador sin backend propio.  
- **Honeypot**: Campo oculto usado para detectar bots.  
- **ARIA live region**: Área del DOM que anuncia cambios de contenido a lectores de pantalla.  
- **WCAG 2.1**: Pautas de accesibilidad web.  

## **Control de Cambios**

| **Versión** | **Fecha**   | **Autor**         | **Descripción de Cambios** |
|-------------|-------------|-------------------|-----------------------------|
| 1.0         | 27/08/2025  | Sergio Aguilar    | Versión inicial             |
