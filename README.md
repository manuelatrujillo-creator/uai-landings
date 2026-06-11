# UAI Landings — Campus Argentina

Repositorio de landing pages de UAI. Cada landing es una página HTML
independiente, con su propio archivo de contenido editable vía Decap CMS.

## Estructura

```
uai-landings/
├── admin/
│   ├── index.html        # Panel de Decap CMS
│   └── config.yml         # Configuración de colecciones/campos editables
├── content/
│   └── uai-diseno-comunicacion-visual.json   # Contenido editable de la landing
├── uai-diseno-comunicacion-visual/
│   └── index.html         # Landing: Lic. en Diseño de Comunicación Visual (Rosario)
├── netlify.toml
└── README.md
```

## Agregar una nueva landing

1. Crear una carpeta nueva (ej. `uai-nombre-carrera/`) con su `index.html`.
2. Agregar `data-cms="<key>"` a los elementos editables del HTML.
3. Crear `content/<slug>.json` con los valores iniciales de esos campos.
4. Copiar al `<body>` el bloque de carga sync-XHR de CMS y el script
   aplicador del final de página (ver `uai-diseno-comunicacion-visual/index.html`
   como referencia), ajustando la ruta del JSON.
5. Agregar una nueva entrada en `admin/config.yml`, bajo `collections > landings > files`,
   apuntando al nuevo `content/<slug>.json` con sus campos.

## Puesta en marcha (GitHub + Netlify)

### 1. GitHub
- Crear el repo `campusargentina/uai-landings` (público o privado).
- Subir el contenido de esta carpeta a la rama `main`.

### 2. Netlify
- "Add new site" → "Import an existing project" → conectar con GitHub → elegir `campusargentina/uai-landings`.
- Build command: vacío. Publish directory: `.` (raíz).
- Una vez creado el sitio: **Site configuration → Identity → Enable Identity**.
- Luego: **Identity → Services → Git Gateway → Enable Git Gateway**.
- En **Identity → Registration**, configurar "Invite only" para que solo el equipo de Campus pueda entrar al CMS.
- Invitar a los editores desde **Identity → Invite users**.

### 3. Acceder al CMS
- Ir a `https://<tu-sitio>.netlify.app/admin/`.
- Iniciar sesión con la invitación de Netlify Identity.
- Editar los campos de la landing y hacer "Publish" — esto genera un commit
  automático en GitHub, que dispara un nuevo deploy en Netlify.
