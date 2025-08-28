# Sitio Freelancer 💻✨

Sitio web estático de portfolio para un **Diseñador y Desarrollador Web Freelancer**.  
Incluye secciones de inicio, sobre mí, contacto y ejemplos de servicios.

---

## 🚀 Características

- **HTML5 + CSS3** con diseño responsive
- **Optimización de imágenes** (JPG y WebP en 640px, 1280px y 1920px)
- **CSS minificado** (`style.min.css`) para producción
- Formularios accesibles con labels conectados
- Preparado para deploy en **Netlify, Vercel o GitHub Pages**

---

## 📂 Estructura del proyecto

```
sitioFreelancer/
├── css/
│   ├── normalize.css
│   ├── style.css        # CSS original
│   └── style.min.css    # CSS minificado (build)
├── img/                 # Imágenes optimizadas (jpg + webp)
├── js/                  # Scripts (vacío por ahora)
├── index.html
├── about.html
├── nosotros.html
├── contacto.html
├── package.json         # Configuración de dependencias
├── postcss.config.cjs   # Configuración PostCSS
└── README.md
```

---

## ⚙️ Instalación y uso en local

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/tuusuario/sitioFreelancer.git
   cd sitioFreelancer
   ```

2. Instalar dependencias:
   ```bash
   npm install
   ```

3. Ejecutar servidor local:
   ```bash
   npm run dev
   ```
   👉 Abre [http://localhost:5173](http://localhost:5173)

4. Construir CSS minificado e imágenes optimizadas:
   ```bash
   npm run build
   ```

---

## 📤 Deploy

Este proyecto es **100% estático**, por lo que puede desplegarse fácilmente en:

- [Netlify](https://netlify.com) → arrastrar carpeta del proyecto
- [Vercel](https://vercel.com) → importar repo desde GitHub
- [GitHub Pages](https://pages.github.com/) → habilitar Pages en Settings

---

## 🛠️ Scripts disponibles

- `npm run dev` → inicia un servidor local con **serve**  
- `npm run css:build` → genera `css/style.min.css` con PostCSS + cssnano  
- `npm run img:hero` → optimiza `img/hero.jpg` en varias resoluciones (JPG y WebP)  
- `npm run build` → ejecuta minificación de CSS y optimización de imágenes  

---

## 👨‍💻 Autor

**Sergio Aguilar**  
📍 La Plata, Buenos Aires  

---

## 📜 Licencia

Este proyecto se distribuye bajo licencia MIT.  
Eres libre de usarlo, modificarlo y desplegarlo.
