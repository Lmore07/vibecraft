# 🚀 VibeCraft Studio — Landing Page

Landing page oficial de **VibeCraft Studio**, un estudio de desarrollo de software y productos digitales de alta gama. Creadores de **DuoLedger**, **QuoteCraft**, **FocusFlow** y **SnapBite**.

Desarrollada con **Astro v5**, **Tailwind CSS v4** y optimizada para despliegue en un **Droplet de DigitalOcean** con Nginx y Docker.

---

## 💻 Desarrollo Local

```bash
# 1. Instalar dependencias
npm install

# 2. Servidor de desarrollo
npm run dev
```
Abre [http://localhost:4321](http://localhost:4321) en tu navegador.

---

## 📦 Compilación para Producción

```bash
npm run build
npm run preview
```

---

## 🌐 Despliegue en Vercel (Recomendado)

Astro está optimizado de forma nativa para **Vercel**:
* Cero configuración de servidores o Nginx.
* Certificado SSL automático (HTTPS).
* CDN global ultra-rápida.

Revisa la guía completa paso a paso en [**VERCEL_DEPLOYMENT.md**](./VERCEL_DEPLOYMENT.md).

```bash
# Despliegue directo por terminal:
npx vercel
```

---

## 🐳 Despliegue Alternativo en Droplet / Docker

Si prefieres usar un servidor VPS o Droplet propio, revisa [**DEPLOYMENT.md**](./DEPLOYMENT.md).

```bash
docker compose up -d --build
```
