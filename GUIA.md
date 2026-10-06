# Guía: publicar tu página estática gratis con Cloudflare Pages

**Costo total: solo el dominio (~$10 USD/año un `.com`).** Hosting, SSL, CDN y DNS son gratis.

---

## Archivos de esta plantilla

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Tu página. Incluye botón de WhatsApp (normal y flotante), metadatos SEO y datos `LocalBusiness` para Google. |
| `robots.txt` | Le dice a Google que puede indexar todo y dónde está el sitemap. |
| `sitemap.xml` | Lista de páginas para que Google las encuentre rápido. |
| `404.html` | Página de error personalizada (Cloudflare la usa automáticamente). |
| `_redirects` | Redirige `www.tudominio.com` → `tudominio.com` (una sola versión canónica). |
| `.gitignore` | Evita subir archivos basura del sistema. |

### Antes de subir, busca y reemplaza en todos los archivos:

- `TUDOMINIO.com` → tu dominio real (está en `index.html`, `robots.txt`, `sitemap.xml`, `_redirects`).
- `523312345678` → tu número de WhatsApp: **52 + 10 dígitos**, sin `+`, espacios ni guiones.
- `33 1234 5678` → tu número tal como quieres que se vea.
- Textos de ejemplo: "Mi Negocio", título, descripción, servicios, dirección, horario, redes sociales.
- Si no tienes imagen de portada, borra las líneas `og:image` e `"image"` del JSON-LD.

> Tip: en VS Code usa **Ctrl+Shift+H** (buscar y reemplazar en toda la carpeta).

---

## Paso 0 — Lo que necesitas

- Un correo electrónico.
- Git instalado: <https://git-scm.com/downloads> (en Windows acepta todo por defecto).
- Opcional pero recomendado: [GitHub Desktop](https://desktop.github.com/) si prefieres no usar la terminal.

---

## Paso 1 — Crear cuenta en GitHub (5 min)

1. Entra a <https://github.com/signup>.
2. Pon tu correo, una contraseña y un nombre de usuario (ej. `juanperez-gdl`).
3. Confirma el código que te llega al correo.
4. Elige el plan **Free**.

### Crear el repositorio (donde vive tu código)

1. Arriba a la derecha, clic en **+** → **New repository**.
2. **Repository name**: `mi-sitio` (o el nombre que quieras, sin espacios).
3. Puede ser **Public** o **Private** (Cloudflare Pages funciona con ambos).
4. **No** marques "Add a README" ni nada más. Clic en **Create repository**.
5. Deja esa página abierta: te mostrará la URL del repo, algo como
   `https://github.com/TU_USUARIO/mi-sitio.git`.

---

## Paso 2 — Subir los archivos a GitHub

### Opción A — Con la terminal (Git)

Abre una terminal **dentro de la carpeta `sitio-web`** (en Windows: clic derecho → "Open Git Bash here" o "Abrir en Terminal") y ejecuta:

```bash
# Solo la primera vez que usas Git en tu computadora
git config --global user.name "Tu Nombre"
git config --global user.email "tu@correo.com"

# Inicializar y subir
git init
git add .
git commit -m "Primera versión del sitio"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/mi-sitio.git
git push -u origin main
```

Al hacer `push` te pedirá iniciar sesión: se abre el navegador, autorizas y listo.
Refresca la página del repo en GitHub y verás tus archivos.

### Opción B — Sin terminal (GitHub Desktop)

1. Instala y abre GitHub Desktop, inicia sesión con tu cuenta.
2. **File → Add local repository** → elige la carpeta `sitio-web`.
   Si dice que no es un repositorio, clic en **create a repository** ahí mismo.
3. Abajo a la izquierda escribe un mensaje (ej. "Primera versión") → **Commit to main**.
4. Arriba, clic en **Publish repository** → quita o deja "Keep this code private" → **Publish**.

### Opción C — Arrastrar y soltar (lo más rápido, sin instalar nada)

1. En la página vacía de tu repo, clic en **uploading an existing file**.
2. Arrastra **todos** los archivos de la carpeta (incluidos `_redirects` y `.gitignore`).
3. Abajo, **Commit changes**.

> Para futuros cambios, la opción A o B es más cómoda: editas, haces commit y push, y el sitio se actualiza solo en ~30 segundos.

---

## Paso 3 — Crear cuenta en Cloudflare (3 min)

1. Entra a <https://dash.cloudflare.com/sign-up>.
2. Correo + contraseña → **Sign Up**. Confirma el correo.
3. Si te pregunta qué quieres hacer, puedes saltarlo ("Skip" / "Explore the dashboard").
4. Recomendado: activa la verificación en dos pasos en **My Profile → Authentication**.

---

## Paso 4 — Publicar el sitio en Cloudflare Pages

1. En el menú izquierdo: **Workers & Pages** → **Create** → pestaña **Pages** → **Connect to Git**.
2. Clic en **Connect GitHub** → autoriza a Cloudflare.
   Puedes darle acceso solo al repo `mi-sitio` ("Only select repositories").
3. Selecciona el repositorio → **Begin setup**.
4. Configuración de build (tu sitio es HTML puro, no hay que compilar nada):
   - **Project name**: `mi-sitio` (esto te da `mi-sitio.pages.dev` gratis).
   - **Production branch**: `main`.
   - **Framework preset**: `None`.
   - **Build command**: déjalo **vacío**.
   - **Build output directory**: `/` (o vacío).
5. **Save and Deploy**. En menos de un minuto tu sitio está en vivo en
   `https://mi-sitio.pages.dev`. Ábrelo y revisa que todo se vea bien.

A partir de ahora, **cada vez que hagas `git push`, Cloudflare vuelve a publicar solo.**

---

## Paso 5 — Comprar el dominio en Cloudflare Registrar

Cloudflare vende al costo (sin ganancia), renueva al mismo precio y la privacidad WHOIS es gratis.
Soporta `.com`, `.mx`, `.com.mx`, `.net`, etc.

1. Menú izquierdo: **Domain Registration** → **Register Domains**.
2. Busca el nombre que quieres. Verás el precio anual (ej. `.com` ≈ $10.44 USD).
3. **Purchase** → llena tus datos de contacto (son obligatorios por ICANN, pero quedan ocultos al público).
4. Paga con tarjeta. Puedes activar **auto-renovación** para no perder el dominio.

> **¿Y si prefieres comprarlo en otro lado?** (Porkbun, Namecheap, Akky, Neubox…)
> Funciona igual. Solo que después tendrás que:
> 1. En Cloudflare: **Add a domain** → escribir tu dominio → plan **Free** → te dará 2 nameservers.
> 2. En tu registrador: cambiar los nameservers por los de Cloudflare.
> 3. Esperar de minutos a 24 h a que se active.
>
> Comprándolo directo en Cloudflare te saltas todo eso.

---

## Paso 6 — Conectar el dominio a tu sitio

1. **Workers & Pages** → tu proyecto `mi-sitio` → pestaña **Custom domains** → **Set up a custom domain**.
2. Escribe `tudominio.com` → **Continue** → **Activate domain**.
   Como el dominio está en Cloudflare, el registro DNS se crea solo.
3. Repite el paso para `www.tudominio.com` (así el archivo `_redirects` puede mandar `www` a la versión sin `www`).
4. En 1–5 minutos el estado pasa a **Active** y tendrás HTTPS automático.

Verifica en el navegador: `https://tudominio.com` y `https://www.tudominio.com` (esta debe redirigir a la primera).

---

## Paso 7 — Que Google te indexe (Search Console)

1. Entra a <https://search.google.com/search-console> con tu cuenta de Google.
2. **Añadir propiedad** → tipo **Dominio** → escribe `tudominio.com` → **Continuar**.
3. Google te dará un registro **TXT** para verificar. Cópialo.
4. En Cloudflare: tu dominio → **DNS** → **Records** → **Add record**:
   - Type: `TXT` · Name: `@` · Content: *(pega el valor de Google)* → **Save**.
5. Regresa a Search Console → **Verificar**. (Si falla, espera 5 min y reintenta).
6. Ya verificado, en el menú izquierdo **Sitemaps** → escribe `sitemap.xml` → **Enviar**.
7. Opcional: en **Inspección de URLs** pega `https://tudominio.com/` → **Solicitar indexación** para acelerar.

Normalmente Google indexa en unos días a un par de semanas. Para comprobarlo busca en Google:
`site:tudominio.com`

### Ajustes en Cloudflare para no bloquear a Google

- Tu dominio → **Security** → **Bots**: deja **Bot Fight Mode desactivado** (puede bloquear a Googlebot).
- No crees reglas de WAF que requieran captcha a todo el tráfico.

### Si eres negocio físico

Date de alta también en **Google Business Profile** (<https://business.google.com>) y pon ahí la misma URL. Es gratis y es lo que más te hace aparecer en Maps y búsquedas locales.

---

## Cómo actualizar el sitio después

```bash
# edita tus archivos, y luego:
git add .
git commit -m "Describe el cambio"
git push
```

Cloudflare detecta el push y publica la nueva versión en ~30 segundos.
Si agregas páginas nuevas, agrégalas también a `sitemap.xml` y actualiza `lastmod`.

---

## Problemas comunes

| Síntoma | Solución |
|---|---|
| El sitio no carga tras conectar el dominio | Espera 5–10 min. Revisa en **Custom domains** que diga *Active*. |
| `www` no redirige | Asegúrate de haber agregado `www.tudominio.com` como custom domain y de que en `_redirects` el dominio esté bien escrito. |
| Cambios que no se ven | Ctrl+F5 en el navegador. Revisa en **Workers & Pages → Deployments** que el último deploy diga *Success*. |
| Search Console no verifica | El registro TXT debe estar en `@` (raíz). Espera unos minutos; el DNS de Cloudflare es rápido pero Google a veces tarda. |
| El botón de WhatsApp dice "número inválido" | Formato: `52` + 10 dígitos, sin `+`, sin espacios, sin `1` extra después del 52. |

---

## Resumen de costos

| Concepto | Costo |
|---|---|
| Hosting (Cloudflare Pages) | $0 |
| SSL / HTTPS | $0 |
| DNS y CDN | $0 |
| GitHub | $0 |
| Google Search Console | $0 |
| **Dominio `.com`** | **≈ $10.44 USD/año** (≈ $190–200 MXN) |
| Dominio `.com.mx` | consulta precio actual en Cloudflare o Akky/Neubox |
