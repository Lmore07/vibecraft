# 🚀 Guía de Despliegue en DigitalOcean Droplet con Dominio Propio

Esta guía explica paso a paso cómo subir la landing page **VibeCraft** a un Droplet de DigitalOcean (Ubuntu) y vincular tu dominio personalizado con certificado SSL gratuito (HTTPS).

---

## 1. Requisitos Previos

1. Un **Droplet en DigitalOcean** (con Ubuntu 22.04 o 24.04, el plan básico de \$4 o \$6/mes es más que suficiente).
2. La **IP pública** de tu Droplet (ej. `143.198.xxx.xxx`).
3. Tu **dominio propio** comprado en cualquier registrador (Namecheap, GoDaddy, Cloudflare, DonDominio, etc.).

---

## 2. Configurar DNS de tu Dominio

Entra al panel de control de tu registrador de dominio o Cloudflare y añade los siguientes registros DNS tipo **A**:

| Tipo | Nombre / Host | Valor (IP de tu Droplet) | TTL |
| :--- | :--- | :--- | :--- |
| **A** | `@` (o tu dominio raíz) | `TU_IP_DEL_DROPLET` | Automático / 300s |
| **A** | `www` | `TU_IP_DEL_DROPLET` | Automático / 300s |

> *Nota: La propagación de DNS suele tardar entre 5 y 30 minutos.*

---

## 3. Conectarse al Droplet y Preparar el Servidor

Conéctate por SSH a tu Droplet desde tu terminal:
```bash
ssh root@TU_IP_DEL_DROPLET
```

Actualiza los paquetes del sistema e instala Docker y Docker Compose:
```bash
# Actualizar repositorios
apt update && apt upgrade -y

# Instalar Docker
apt install -y docker.io docker-compose-plugin git

# Iniciar y habilitar Docker
systemctl start docker
systemctl enable docker
```

---

## 4. Subir el Código de VibeCraft al Droplet

Tienes dos formas sencillas de subir el proyecto:

### Opción A: Mediante Git (Recomendada)
Sube tu carpeta `Z:\Proyectos\vibecraft` a tu repositorio de GitHub / GitLab y luego en el Droplet clónala:
```bash
cd /var/www
git clone https://github.com/tu-usuario/vibecraft.git
cd vibecraft
```

### Opción B: Mediante SCP (Copia directa desde Windows)
Desde tu terminal en Windows:
```powershell
scp -r "Z:\Proyectos\vibecraft" root@TU_IP_DEL_DROPLET:/var/www/vibecraft
```
Y luego en el Droplet:
```bash
cd /var/www/vibecraft
```

---

## 5. Levantar el Contenedor con Docker Compose

Dentro de la carpeta `/var/www/vibecraft`:
```bash
docker compose up -d --build
```

Verifica que el contenedor esté corriendo:
```bash
docker ps
```
¡Listo! Si abres `http://TU_IP_DEL_DROPLET` en tu navegador, ya verás la landing page de VibeCraft funcionando con Nginx a máxima velocidad.

---

## 6. Configurar SSL Gratis (HTTPS) con Certbot / Nginx Proxy

Para que tu dominio tenga el candado verde seguro (`https://tudominio.com`):

### Método Rápido con Nginx en el Host:
Si prefieres que Nginx en el host maneje el SSL y redirija al contenedor:

1. Instalar Certbot:
   ```bash
   apt install -y certbot python3-certbot-nginx nginx
   ```
2. Crear un archivo de configuración para tu dominio en `/etc/nginx/sites-available/vibecraft`:
   ```nginx
   server {
       server_name tudominio.com www.tudominio.com;

       location / {
           proxy_pass http://localhost:80;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```
3. Activar el sitio:
   ```bash
   ln -s /etc/nginx/sites-available/vibecraft /etc/nginx/sites-enabled/
   nginx -t
   systemctl restart nginx
   ```
4. Emitir certificado SSL con un solo comando:
   ```bash
   certbot --nginx -d tudominio.com -d www.tudominio.com
   ```
   *Certbot configurará automáticamente la renovación de certificados cada 90 días.*

---

## 7. Comandos Útiles de Mantenimiento

* **Ver logs en tiempo real:**
  ```bash
  docker compose logs -f
  ```
* **Actualizar cambios de código:**
  ```bash
  git pull
  docker compose up -d --build
  ```
* **Reiniciar el contenedor:**
  ```bash
  docker compose restart
  ```
