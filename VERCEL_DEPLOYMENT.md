# 🚀 Guía de Despliegue en Vercel con Dominio Propio

Subir **VibeCraft** a **Vercel** es incluso **más fácil, rápido y potente** que en un Droplet:
- ⚡ **Global CDN (Edge):** El sitio carga en menos de 100 ms en cualquier parte del mundo.
- 🔒 **SSL Automático:** Certificado HTTPS gratis sin configurar Certbot ni Nginx.
- 🔄 **CI/CD Automático:** Cada vez que hagas `git push`, tu web se actualiza sola en segundos.
- 🌐 **Dominio Propio en 2 clics:** Vercel te da las DNS exactas para vincular tu dominio al instante.
- 💰 **Costo \$0 (Plan Hobby):** Completamente gratis.

---

## Opción 1: Despliegue mediante GitHub (La más recomendada)

### Paso 1: Subir el proyecto a GitHub
Desde tu terminal en `Z:\Proyectos\vibecraft`:

```bash
cd Z:\Proyectos\vibecraft

# 1. Inicializar git si aún no lo tienes
git init

# 2. Agregar todos los archivos
git add .

# 3. Hacer el commit inicial
git commit -m "feat: landing page vibecraft studio"

# 4. Vincular a tu repositorio de GitHub (crea un repo vacío en github.com)
git branch -M main
git remote add origin https://github.com/TU_USUARIO/vibecraft.git
git push -u origin main
```

### Paso 2: Importar en Vercel
1. Entra a [vercel.com](https://vercel.com) e inicia sesión con tu cuenta de GitHub.
2. Haz clic en **"Add New..."** ➔ **"Project"**.
3. Selecciona tu repositorio `vibecraft` y presiona **"Import"**.
4. Vercel detectará automáticamente:
   - **Framework Preset:** `Astro`
   - **Build Command:** `astro build`
   - **Output Directory:** `dist`
5. Haz clic en el botón azul **"Deploy"**.
6. En menos de 45 segundos, tu web estará online con una URL tipo `vibecraft-xxx.vercel.app`.

---

## Opción 2: Despliegue directo desde la terminal (En 1 minuto)

Si no quieres usar GitHub ahora mismo, puedes desplegar directo desde tu consola:

```bash
cd Z:\Proyectos\vibecraft

# Ejecutar el CLI de Vercel
npx vercel
```

1. Te pedirá iniciar sesión o confirmar tu cuenta en el navegador.
2. Responde las preguntas por defecto:
   - *Set up and deploy?* ➔ `Y`
   - *Which scope?* ➔ Tu cuenta personal
   - *Link to existing project?* ➔ `N`
   - *Project name?* ➔ `vibecraft`
   - *Directory?* ➔ `./`
3. ¡Listo! Te devolverá la URL de producción de inmediato.

---

## 🌐 Cómo Conectar tu Dominio Personalizado en Vercel

1. En el panel de tu proyecto en Vercel, ve a **Settings** ➔ **Domains**.
2. Escribe tu dominio (ej. `tudominio.com`) y haz clic en **Add**.
3. Vercel te mostrará los registros DNS recomendados:
   - **Para el dominio raíz (`tudominio.com`):**  
     Un registro **A** apuntando a `76.76.21.21`
   - **Para el subdominio `www` (`www.tudominio.com`):**  
     Un registro **CNAME** apuntando a `cname.vercel-dns.com`
4. Agrégalos en el panel de tu registrador de dominios (Cloudflare, Namecheap, GoDaddy, etc.).
5. Vercel verificará las DNS en 1 o 2 minutos y emitirá automáticamente tu certificado SSL (HTTPS).
