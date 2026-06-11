# Guía paso a paso — Publicar la landing con GitHub + Netlify + Decap CMS

Esta guía asume que ya tenés la carpeta `uai-landings/` (la que te compartí) en tu computadora.

## 1. Crear el repositorio en GitHub

1. Entrá a https://github.com/campusargentina (o la cuenta/organización correspondiente).
2. "New repository" → nombre: `uai-landings`.
3. Dejalo vacío (sin README, sin .gitignore — ya tenemos los archivos).
4. Creá el repo.
5. Subí el contenido de la carpeta `uai-landings/` a la rama `main`. Si tenés Git instalado, desde la carpeta:
   ```
   git init
   git add .
   git commit -m "Landing UAI Diseño de Comunicación Visual + CMS"
   git branch -M main
   git remote add origin https://github.com/campusargentina/uai-landings.git
   git push -u origin main
   ```
   Si no usás la terminal, también podés arrastrar los archivos/carpetas directamente desde la interfaz web de GitHub ("Add file" → "Upload files"), respetando la estructura de carpetas.

## 2. Crear el sitio en Netlify

1. Entrá a https://app.netlify.com.
2. "Add new site" → "Import an existing project".
3. Conectá tu cuenta de GitHub (si no lo hiciste antes) y elegí el repo `campusargentina/uai-landings`.
4. Configuración del build:
   - **Build command:** dejar vacío.
   - **Publish directory:** `.` (la raíz del repo).
5. "Deploy site". En unos segundos vas a tener una URL tipo `https://random-name-123.netlify.app`.
6. (Opcional) Cambiar el nombre del sitio: Site configuration → General → "Change site name".

## 3. Activar Identity (login para el CMS)

1. En el panel del sitio: **Site configuration → Identity → Enable Identity**.
2. En **Registration preferences**, elegí **"Invite only"** (así solo entra quien vos invites).
3. Bajá a **Services → Git Gateway → Enable Git Gateway**. Esto le da permiso a Decap para escribir commits en tu repo sin que cada editor necesite su propia cuenta de GitHub.

## 4. Invitar a los editores

1. **Identity → Invite users**.
2. Cargá el email de cada persona que va a editar contenido (vos, otros miembros del equipo de marketing, etc.).
3. Cada invitado recibe un mail para definir su contraseña.

## 5. Usar el CMS

1. Andá a `https://<tu-sitio>.netlify.app/admin/`.
2. Iniciá sesión con tu usuario de Netlify Identity.
3. Vas a ver la colección **"Landings"** → entrá a **"UAI · Lic. en Diseño de Comunicación Visual (Rosario)"**.
4. Editá cualquiera de los ~60 campos disponibles (descuentos, textos del hero, características, secciones de "sobre la carrera", áreas de desempeño, testimonio, footer, WhatsApp, etc.).
5. Click en **"Publish"**. Esto:
   - Genera un commit automático en el repo de GitHub.
   - Dispara un nuevo deploy en Netlify (tarda ~1 min).
6. Refrescá la landing pública para ver los cambios.

## 6. Agregar una nueva landing (a futuro)

1. Duplicar la carpeta `uai-diseno-comunicacion-visual/` con un nuevo nombre (ej. `uai-otra-carrera/`).
2. Crear `content/<nuevo-slug>.json` con los valores iniciales.
3. En el HTML nuevo, agregar `data-cms="<key>"` a los elementos editables y ajustar la ruta del JSON en el script de carga (`/content/<nuevo-slug>.json`).
4. Sumar una entrada nueva en `admin/config.yml`, dentro de `collections > landings > files`, apuntando al nuevo JSON con sus campos.
5. Commitear y pushear — Netlify hace el resto.

---

## Notas

- **Algunos campos admiten HTML simple** (`<br>`, `<em>`, `<span>`) porque así están en el diseño original — si los editás, mantené esas etiquetas si querés conservar el salto de línea o el resaltado de color. Estos campos están marcados en `config.yml` con comentarios indicando "admite <br>" etc.
- **No hay conector de GitHub disponible** en este entorno, así que los pasos 1 y los futuros pushes los tenés que hacer vos (o pedirle a alguien del equipo técnico). Una vez conectado el repo a Netlify, las publicaciones desde el CMS sí son automáticas.
- Si en algún momento el campo `/content/<slug>.json` no carga (por ejemplo, abriendo el HTML como archivo local sin servidor), la landing usa los valores que ya están escritos directamente en el HTML como respaldo — nunca se rompe.
