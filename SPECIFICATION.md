# 🌐 VibeCraft Studio - Landing Page & Web Showcase

Documento de especificación técnica, sistema de diseño, módulos interactivos y directrices de desarrollo para la landing page oficial de **VibeCraft** (`vibecraft.dev` / `vibecraft.app`).

---

## 1. Configuración del Entorno y Setup

### 1.1. Tecnologías Base
* **Framework:** [Astro v5](https://astro.build/) (Static Site Generation ultra-rápido, Core Web Vitals optimizados, cero sobrecarga de JavaScript).
* **Estilos:** Tailwind CSS v4 con `@tailwindcss/vite` e integración de paleta cromática exacta de DuoLedger.
* **Servidor de Producción:** Nginx Alpine optimizado con compresión Gzip y headers de caché inmutable.
* **Contenedor:** Docker y Docker Compose para despliegue en 1 comando en DigitalOcean Droplets.

### 1.2. Comandos de Desarrollo y Compilación Local
```bash
cd Z:\Proyectos\vibecraft

# 1. Instalar dependencias
npm install

# 2. Iniciar servidor de desarrollo local (http://localhost:4321)
npm run dev

# 3. Compilar para producción (genera carpeta dist/)
npm run build

# 4. Probar build estático localmente
npm run preview
```

---

## 2. Sistema de Diseño (UX / UI Design System)

Inspirado directamente en la estética visual y calidez de **DuoLedger**:

### 2.1. Paleta de Colores
* **Primary (Lavanda / Índigo Moderno):** `#6366F1` (Acento principal, botones, gradientes).
* **Primary Dark:** `#4F46E5`.
* **Primary Light:** `#EEF2FF` (Fondo de insignias y selecciones).
* **Secondary (Rosa Afectivo / Coral):** `#F43F5E` (Detalles de pareja, acentos cálidos).
* **Positive (Verde Menta):** `#10B981` (Indicador de balance a favor, estado sincronizado en tiempo real).
* **Negative (Naranja Cálido):** `#F97316` (Gastos pendientes, atención).
* **Superficies & Fondos:** `#FFFFFF` (Tarjetas), `#F8FAFC` (Fondo general descansado), `#0F172A` (Sección oscura de stack tecnológico y footer).

### 2.2. Tipografía y Radios de Borde
* **Tipografía:** *Plus Jakarta Sans* para encabezados de alto impacto visual y *Inter / System* para textos de lectura.
* **Bordes Redondeados:** Radios generosos de `24px` a `32px` (siguiendo el estándar moderno de iOS y la app de DuoLedger).
* **Efectos:** *Glassmorphism* sutil con `backdrop-blur-md` y bordes de `1.2px solid #F1F5F9`.

---

## 3. Módulos y Secciones de la Landing Page

1. **Header / Navbar:**
   * Logotipo de VibeCraft Studio con degradado característico.
   * Navegación fluida anclada con `scroll-behavior: smooth`.
   * Botón de contacto directo a WhatsApp con mensaje precargado.
   * Menú desplegable responsivo para móviles.

2. **Hero Section:**
   * Titular de alto impacto enfocado en estudio de ingeniería de software.
   * Badges de credibilidad ("Creadores de DuoLedger", "Sync WebSockets", "Flutter iOS & Android").
   * Botones de acción directa con sombra de resplandor.

3. **DuoLedger Showcase (Pieza Central):**
   * Maqueta hiperrealista de smartphone mostrando la interfaz real de DuoLedger.
   * Tarjeta de balance en tiempo real ("Te deben $65.25 USD", indicador verde menta).
   * Feed de transacciones con iconos de categorías (Supermercado, Cena Italiana, Streaming).
   * Indicador de conexión en tiempo real con WebSockets.
   * Lista de beneficios clave alrededor del teléfono (Sync en milisegundos, divisiones 50/50 y proporcionales, VaultS3 seguro).

4. **Simulador Interactivo de División de Gastos:**
   * Calculadora interactiva en JavaScript donde los visitantes pueden ingresar un monto (ej. $120), alternar entre modos de división (50/50, 60/40, 70/30) y ver el resultado exacto con las tarjetas de estado de DuoLedger.

5. **Suite de Productos VibeCraft:**
   * Muestra del ecosistema completo: DuoLedger (Beta lista), QuoteCraft (B2B técnicos), FocusFlow (Productividad TDAH) y SnapBite (IA Calorie Tracker).

6. **Stack Tecnológico:**
   * Sección oscura de alta sofisticación técnica destacando Flutter, NestJS, PostgreSQL, Socket.io, VaultS3 y Docker.

7. **Servicios de Ingeniería para Clientes:**
   * Oferta para desarrollo de apps a medida, arquitectura en tiempo real y DevOps.

8. **Formulario de Contacto & Footer:**
   * Formulario directo para solicitar acceso a la beta de DuoLedger o cotizar desarrollos, enlace a WhatsApp y derechos reservados.

---

## 4. Esquema de Directorios (Folder Structure)

```
vibecraft/
├── dist/                           # Salida estática compilada por Astro (HTML, CSS, JS)
├── public/                         # Archivos públicos accesibles directamente
│   ├── icons/
│   │   └── icono_duoledger.png     # Icono oficial de DuoLedger
│   ├── images/
│   │   └── logo_duoledger_transparente.png # Logo con fondo transparente
│   └── favicon.svg
├── src/
│   ├── components/                 # Componentes modulares de la página
│   │   ├── Navbar.astro            # Barra de navegación fija con menú móvil
│   │   ├── Hero.astro              # Sección principal con titular y métricas
│   │   ├── DuoLedgerShowcase.astro # Maqueta de smartphone e interfaz de DuoLedger
│   │   ├── InteractiveCalculator.astro # Simulador interactivo de división de gastos
│   │   ├── ProductSuite.astro      # Catálogo de las 4 apps de VibeCraft
│   │   ├── TechStack.astro         # Sección técnica (Flutter, NestJS, Postgres, S3)
│   │   ├── StudioCapabilities.astro# Servicios ofrecidos por la empresa
│   │   ├── ContactSection.astro    # Formulario y llamada a la acción
│   │   └── Footer.astro            # Pie de página y enlaces
│   ├── layouts/
│   │   └── Layout.astro            # Plantilla HTML con SEO, OpenGraph y fuentes
│   ├── pages/
│   │   └── index.astro             # Entrada principal que ensambla la landing
│   └── styles/
│       └── global.css              # Configuración de Tailwind CSS y variables DuoLedger
├── Dockerfile                      # Multi-stage build con Nginx para producción
├── docker-compose.yml              # Configuración de servicio para el Droplet
├── nginx.conf                      # Servidor web Nginx con gzip y caché
├── DEPLOYMENT.md                   # Guía paso a paso para DigitalOcean y dominio SSL
├── SPECIFICATION.md                # Esta especificación
├── astro.config.mjs                # Configuración de Astro y plugin Tailwind
├── package.json
└── tsconfig.json
```
