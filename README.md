# Meowney — control de gastos e ingresos 🐱

App web estática (un solo `index.html`, sin build ni servidor). Se puede instalar en el celular desde el navegador y funciona sin internet.
Trae dos temas, que se cambian en ⚙︎ Ajustes → **Tema**: **Gatitos 🐱** (el diseño kawaii) y **Clásico**.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Toda la app (código, estilos y lógica) |
| `manifest.webmanifest` | Datos para instalarla (nombre, iconos, colores) |
| `sw.js` | Service worker: guarda la app para usarla sin internet |
| `favicon.svg`, `favicon.ico`, `favicon-16.png`, `favicon-32.png` | Icono de la pestaña del navegador (gatito kawaii) |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png` | Iconos de la app instalada |
| `vercel.json` | Configuración de Vercel (cabeceras) |

> Importante: **todos los archivos tienen que quedar en la raíz** del proyecto (junto a `index.html`), no dentro de una subcarpeta.

## Subirla a Vercel

Vercel no necesita configuración: no hay comando de build ni carpeta de salida.

### Opción A — Con GitHub (la más cómoda para actualizar después)
1. Crea un repositorio y sube **todos** estos archivos a la raíz.
2. En [vercel.com](https://vercel.com) → **Add New… → Project** → importa el repositorio.
3. Deja **Framework Preset: Other**, sin Build Command ni Output Directory. Pulsa **Deploy**.
4. Cada vez que cambies algo y hagas `git push`, Vercel publica la nueva versión sola.

### Opción B — Con la terminal
```bash
npm install -g vercel
cd carpeta-con-los-archivos     # donde están index.html y vercel.json
vercel                          # primera vez: inicia sesión y acepta los valores por defecto
vercel --prod                   # publica en producción
```

> Revisa en vercel.com/pricing las condiciones vigentes del plan gratuito (Hobby): pueden cambiar.

## Si Vercel muestra "404: NOT_FOUND"
Casi siempre significa que `index.html` **no está en la raíz** de lo que Vercel publicó.
1. En Vercel abre el proyecto → **Deployments** → el último despliegue → pestaña **Source** y comprueba que `index.html` aparece **al principio de la lista**, no dentro de una carpeta.
2. Si está dentro de una carpeta: **Settings → General → Root Directory** → escribe el nombre de esa carpeta y vuelve a desplegar. O mueve los archivos a la raíz del repositorio.
3. En **Settings → Build and Deployment**: Framework Preset en **Other**, y **Build Command** y **Output Directory** vacíos.

## Instalarla en el celular
La instalación se hace desde el menú del navegador:
- **Chrome / Brave (Android):** abre tu dirección de Vercel → menú ⋮ → **Instalar aplicación** (o *Añadir a pantalla de inicio*).
- **Safari (iPhone):** botón Compartir → **Añadir a pantalla de inicio**.

## Pasar tus datos desde la versión de Claude
Los datos viven en el navegador **de cada dirección web**, así que la app nueva empieza vacía.
1. En la versión anterior: ⚙︎ → **Exportar** → **Descargar** (o **Copiar respaldo**).
2. En la nueva: ⚙︎ → **Importar** → elige el archivo o pega el texto → **Reemplazar**.

## Cosas a tener en cuenta
- Los datos se guardan en `localStorage` del navegador: no se sincronizan entre dispositivos y se pierden si borras los datos del sitio. **Haz respaldos de vez en cuando.**
- Si cambias la dirección (dominio) de la app, tendrás que exportar e importar de nuevo.
- Para que todos los dispositivos descarguen una versión nueva tras una actualización, cambia `VERSION` en `sw.js` (por ejemplo a `meowney-v3`).
- Si el icono de la pestaña no cambia, recarga con Ctrl+F5: los navegadores guardan los iconos en caché.
