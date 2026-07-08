# Landing pages de dominios

Plantilla reutilizable (HTML + Tailwind vía CDN, sin build) para vender/arrendar dominios. Cada dominio es una copia de `index.html` con el bloque `CONFIG` editado.

## Configurar el formulario (Web3Forms)

1. Ve a https://web3forms.com y genera una **Access Key** gratis con tu email (no requiere cuenta).
2. En `index.html`, busca la línea:
   ```html
   <input type="hidden" name="access_key" value="YOUR_WEB3FORMS_ACCESS_KEY" />
   ```
   y reemplaza `YOUR_WEB3FORMS_ACCESS_KEY` por tu key real.
3. Las consultas llegarán al email con el que creaste la key. Puedes agregar más destinatarios desde el dashboard de Web3Forms.

## Crear una landing para otro dominio

1. Duplica `index.html` (ej: `index-otrodominio.html`, o una carpeta `otrodominio/index.html` si vas a tener varias rutas).
2. Edita el objeto `CONFIG` al final del archivo (dentro del `<script>`):
   - `brand` / `brandTld`: marca que se muestra en el header/footer.
   - `domain` / `domainTld`: el dominio en venta (ej: `coseche` / `.cl`).
   - `tagline`, `tags`, `idealParaText`, `features`: textos de marketing.
   - `priceSale`, `priceRent`: precios mostrados (formato texto, ej `"950.000"`).
3. Actualiza el `<title>` y el `<meta name="description">` en el `<head>` para SEO.
4. Todo el resto del HTML se rellena automáticamente desde `CONFIG` — no hace falta tocar el markup.

## Desplegar en Cloudflare Pages

1. Sube esta carpeta a un repositorio de GitHub/GitLab (o usa `Wrangler`/subida directa de Cloudflare Pages).
2. En Cloudflare Pages: **Create a project** → conecta el repo.
3. Build settings:
   - Framework preset: `None`
   - Build command: (vacío)
   - Build output directory: `/` (raíz, ya que es HTML estático)
4. Deploy. Si tienes múltiples dominios como páginas separadas, cada uno puede ser:
   - Un proyecto de Cloudflare Pages distinto (dominio custom apuntando a cada proyecto), o
   - Una ruta dentro del mismo proyecto (ej: `/coseche/index.html`, `/otrodominio/index.html`).

## Notas

- Tailwind se carga vía CDN (`cdn.tailwindcss.com`) — perfecto para un sitio estático simple, sin paso de build. Si en el futuro quieres optimizar el peso de la página, se puede migrar a Tailwind CLI/build, pero no es necesario para este caso de uso.
- El formulario incluye un campo honeypot (`botcheck`) oculto para reducir spam automático.
