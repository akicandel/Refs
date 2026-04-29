# REF — Archivo de Referencias

Web estática con grid filtrable de referencias de arte y diseño.  
Las referencias se gestionan desde **Google Sheets** — editas la hoja y la web se actualiza sola.

---

## Setup (5 minutos)

### 1. Crea la Google Sheet

Crea una hoja nueva en [Google Sheets](https://sheets.google.com) con estas columnas exactas en la fila 1:

| name | url | cat |
|------|-----|-----|
| Grilli Type | https://www.grillitype.com/ | Fonts |
| Studio Puhl | https://studiopuhl.com/work | Illustration |
| Buck | https://buck.co/ | 3D / CGI |

Las columnas deben llamarse exactamente `name`, `url`, `cat` (en minúsculas).

---

### 2. Publica la hoja como CSV

1. En Google Sheets: **Archivo → Compartir → Publicar en la web**
2. En el desplegable izquierdo selecciona **Hoja 1**
3. En el desplegable derecho selecciona **Valores separados por comas (.csv)**
4. Click en **Publicar** → confirma
5. Copia la URL que aparece — tendrá este formato:
   ```
   https://docs.google.com/spreadsheets/d/XXXXXXXXXX/pub?gid=0&single=true&output=csv
   ```
6. El **Sheet ID** es la parte `XXXXXXXXXX` entre `/d/` y `/pub`

---

### 3. Pon el Sheet ID en el HTML

Abre `index.html` y busca esta línea cerca del principio del `<script>`:

```js
const SHEET_ID = 'TU_SHEET_ID_AQUI';
```

Sustitúyela por tu ID:

```js
const SHEET_ID = 'XXXXXXXXXX';
```

---

### 4. Sube a GitHub Pages

1. Sube `index.html` a tu repositorio de GitHub
2. Ve a **Settings → Pages → Source: main / root**
3. En 1-2 minutos estará en `https://tuusuario.github.io/tu-repo/`

---

## Añadir o editar referencias

Solo tienes que editar la Google Sheet — añadir filas, cambiar nombres, categorías, etc.  
La web carga el CSV en cada visita, así que los cambios se ven inmediatamente sin tocar el código.

### Categorías disponibles

Puedes usar cualquier categoría — si es nueva, la web le asigna un color automáticamente.  
Las categorías actuales son:

`Fonts` · `Illustration` · `Animation` · `Design` · `3D / CGI` · `Typography` · `Art` · `Video` · `Film` · `Foto` · `Craft` · `Mockup` · `Arquitectura` · `Designs` · `Experience` · `Mindful` · `Spaces` · `Industrial` · `Inspiration` · `Color` · `NFT`

---

## Cómo funciona

- La web lee el CSV de Google Sheets en cada carga
- Para cada referencia extrae la imagen OG (`og:image`) de la web real usando proxies CORS públicos
- Las imágenes se cargan de forma lazy (solo cuando la card entra en pantalla)
- Todo es HTML/CSS/JS puro — sin build, sin dependencias, sin backend
