# AURA ESTÉTICA & Bienestar 🌸

Este es un sitio web moderno, elegante y totalmente responsivo para **AURA ESTÉTICA**, diseñado en React con Vite y Tailwind CSS, y optimizado para ser subido a GitHub y alojado en **GitHub Pages**.

---

## 🚀 Cómo subir este proyecto a GitHub y activarlo gratis

Para publicar tu página web en GitHub y que esté visible para todo el mundo, sigue estos sencillos pasos:

### Paso 1: Descargar el código desde AI Studio
1. En la esquina superior derecha de **AI Studio**, haz clic en el menú de **Ajustes** (icono de engranaje o menú de opciones).
2. Selecciona **Exportar** o **Descargar ZIP** para obtener el código fuente completo de tu aplicación en tu computadora.
3. Descomprime el archivo `.zip` en una carpeta de tu elección.

---

### Paso 2: Crear un repositorio en GitHub
1. Entra a tu cuenta de [GitHub](https://github.com/) (si no tienes una, créala gratis).
2. Haz clic en el botón **New** (Nuevo repositorio) en la sección de repositorios.
3. Asígnale un nombre (por ejemplo: `aura-estetica`).
4. Déjalo como **Public** (Público) para poder activar la versión web gratis.
5. No marques ninguna opción de inicialización (como agregar README o `.gitignore`) y haz clic en **Create repository**.

---

### Paso 3: Subir los archivos a tu repositorio
Tienes dos formas de subir el código a GitHub:

#### Opción A: Desde la web de GitHub (La más fácil si no usas Git en tu computadora)
1. En la página de tu nuevo repositorio vacío, verás un enlace que dice *"uploading an existing file"* (subir un archivo existente). Haz clic ahí.
2. Selecciona todos los archivos de la carpeta descomprimida (asegúrate de arrastrar todos los archivos y carpetas, incluyendo `package.json`, `src`, `public`, `index.html`, etc.) y arrástralos a la ventana de GitHub.
3. Espera a que se carguen todos los archivos.
4. En la parte inferior, haz clic en el botón verde **Commit changes** (Confirmar cambios).

#### Opción B: Usando la terminal (Git)
Abre la terminal en la carpeta descomprimida de tu proyecto y ejecuta los siguientes comandos reemplazando `TU_USUARIO` y `TU_REPOSITORIO` con tus datos:
```bash
git init
git add .
git commit -m "Primer commit - Aura Estética"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/TU_REPOSITORIO.git
git push -u origin main
```

---

### Paso 4: Configurar el despliegue automático con GitHub Actions (Recomendado)
Para que GitHub compile y publique tu sitio web automáticamente cada vez que hagas cambios, utilizaremos una **GitHub Action** oficial de Vite:

1. Dentro de tu repositorio en GitHub, ve a la pestaña **Settings** (Configuración).
2. En el menú de la izquierda, selecciona **Pages**.
3. En la sección **Build and deployment**, bajo **Source**, cambia de `Deploy from a branch` a **`GitHub Actions`**.
4. ¡Listo! Ahora crearemos el archivo de flujo de trabajo. En tu computadora, crea una carpeta llamada `.github` y dentro de ella otra llamada `workflows`. Dentro de esta última carpeta, crea un archivo llamado `deploy.yml` con el siguiente contenido:

```yaml
name: Deploy static content to Pages

on:
  push:
    branches: ["main"]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Set up Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

5. Sube estos nuevos archivos a tu repositorio de GitHub. ¡GitHub compilará el código y publicará tu página web automáticamente!
6. Podrás ver la dirección web de tu página en la misma pestaña **Settings -> Pages**.

---

### Paso 5: Opción alternativa de despliegue (Despliegue Manual Rápido)
Si prefieres compilar la página en tu computadora y subir los archivos ya compilados:

1. Abre la terminal en la carpeta de tu proyecto.
2. Instala las dependencias y compila el proyecto ejecutando:
   ```bash
   npm install
   npm run build
   ```
3. Esto generará una carpeta llamada `dist`.
4. El contenido completo de la carpeta `dist` (los archivos dentro de ella) es tu página web estática lista. Puedes subir esos archivos directamente a servicios gratuitos de hosting estático rápido como:
   - **Vercel** ([vercel.com](https://vercel.com/))
   - **Netlify** ([netlify.com](https://netlify.com/))
   - **GitHub Pages** (subiendo la carpeta `dist` directamente a una rama llamada `gh-pages` o arrastrando los archivos de `dist` a un nuevo repositorio).

---

## 🛠️ Tecnologías Utilizadas

- **React 19** con **Vite** para una carga ultra rápida.
- **Tailwind CSS 4** para un diseño visualmente refinado, estética moderna con efectos de panel de vidrio (*glassmorphism*) y tipografía equilibrada.
- **Motion** para transiciones suaves y micro-animaciones profesionales.
- **Lucide React** para un conjunto de iconos modernos y consistentes.
- **Local Storage** integrado para persistir el historial de turnos reservados por la clienta de forma local y offline.
