# 🎧 LANXESS - PROTECCIÓN AUDITIVA PWA
## 📦 CÓDIGO COMPLETO DEL PROYECTO

Este documento contiene TODO el código necesario para tu proyecto.

---

## 📁 ESTRUCTURA DEL PROYECTO

```
lanxess-proteccion-auditiva/
├── public/
│   ├── Sonidos_De_Fabrica.wav          ← TU ARCHIVO (ya lo tienes)
│   ├── microsoft_headphones_surface_2-v1.glb  ← TU ARCHIVO (ya lo tienes)
│   ├── manifest.json
│   └── sw.js
├── src/
│   ├── main.jsx
│   ├── App.jsx
│   ├── index.css
│   └── components/
│       ├── SplashScreen.jsx
│       ├── Onboarding.jsx
│       ├── ExperienciaInmersiva.jsx
│       ├── MensajeFinal.jsx
│       ├── MedidorReal.jsx
│       ├── Navegacion.jsx
│       └── InstallPrompt.jsx
├── index.html
├── package.json
├── vite.config.js
├── netlify.toml
└── README.md
```

---

## ⚙️ PASO 1: INSTALACIÓN INICIAL

### 1.1 Crear el proyecto con Vite

```bash
npm create vite@latest lanxess-proteccion-auditiva -- --template react
cd lanxess-proteccion-auditiva
```

### 1.2 Instalar TODAS las dependencias

```bash
npm install three @react-three/fiber @react-three/drei framer-motion zustand react-confetti howler
npm install -D vite-plugin-pwa
```

---

## 📄 ARCHIVO 1: package.json

**Ubicación:** `/package.json`

```json
{
  "name": "lanxess-proteccion-auditiva-pwa",
  "private": true,
  "version": "1.0.0",
  "type": "module",
  "description": "Progressive Web App para educación en protección auditiva - LANXESS Corporation",
  "author": "Proyecto Educativo LANXESS",
  "license": "MIT",
  "scripts": {
    "dev": "vite --host",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "three": "^0.160.0",
    "@react-three/fiber": "^8.15.0",
    "@react-three/drei": "^9.92.0",
    "@react-three/postprocessing": "^2.15.0",
    "framer-motion": "^10.16.16",
    "zustand": "^4.4.7",
    "react-confetti": "^6.1.0",
    "howler": "^2.2.4",
    "react-spring": "^9.7.3",
    "canvas-confetti": "^1.9.2"
  },
  "devDependencies": {
    "@types/react": "^18.2.43",
    "@types/react-dom": "^18.2.17",
    "@types/three": "^0.160.0",
    "@vitejs/plugin-react": "^4.2.1",
    "autoprefixer": "^10.4.16",
    "eslint": "^8.55.0",
    "eslint-plugin-react": "^7.33.2",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.5",
    "postcss": "^8.4.32",
    "tailwindcss": "^3.4.0",
    "vite": "^5.0.8",
    "vite-plugin-pwa": "^0.17.4"
  }
}
```

**Después de crear este archivo, ejecuta:**
```bash
npm install
```

---

## 📄 ARCHIVO 2: vite.config.js

**Ubicación:** `/vite.config.js`

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import { VitePWA } from 'vite-plugin-pwa'

export default defineConfig({
  plugins: [
    react(),
    VitePWA({
      registerType: 'autoUpdate',
      includeAssets: ['*.wav', '*.glb', '*.png', '*.jpg', '*.svg'],
      manifest: {
        name: 'LANXESS - Protección Auditiva',
        short_name: 'LANXESS Audio',
        description: 'Experiencia inmersiva para educación en protección auditiva',
        theme_color: '#1a1a2e',
        background_color: '#0f0f1e',
        display: 'standalone',
        scope: '/',
        start_url: '/',
        orientation: 'portrait',
        icons: [
          {
            src: '/icon-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: '/icon-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          },
          {
            src: '/icon-512x512.png',
            sizes: '512x512',
            type: 'image/png',
            purpose: 'any maskable'
          }
        ]
      },
      workbox: {
        globPatterns: ['**/*.{js,css,html,ico,png,svg,wav,glb}'],
        runtimeCaching: [
          {
            urlPattern: /^https:\/\/fonts\.googleapis\.com\/.*/i,
            handler: 'CacheFirst',
            options: {
              cacheName: 'google-fonts-cache',
              expiration: {
                maxEntries: 10,
                maxAgeSeconds: 60 * 60 * 24 * 365
              },
              cacheableResponse: {
                statuses: [0, 200]
              }
            }
          }
        ]
      }
    })
  ],
  server: {
    host: true,
    port: 3000
  },
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          'react-vendor': ['react', 'react-dom'],
          'three-vendor': ['three', '@react-three/fiber', '@react-three/drei'],
          'animation-vendor': ['framer-motion']
        }
      }
    }
  }
})
```

---

## 📄 ARCHIVO 3: netlify.toml

**Ubicación:** `/netlify.toml`

```toml
[build]
  command = "npm run build"
  publish = "dist"
  environment = { NODE_VERSION = "18" }

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-Content-Type-Options = "nosniff"
    X-XSS-Protection = "1; mode=block"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Service-Worker-Allowed = "/"
    Access-Control-Allow-Origin = "*"

[[headers]]
  for = "/*.wav"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
    Content-Type = "audio/wav"

[[headers]]
  for = "/*.glb"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
    Content-Type = "model/gltf-binary"

[[headers]]
  for = "/sw.js"
  [headers.values]
    Cache-Control = "no-cache, no-store, must-revalidate"
    Content-Type = "application/javascript"
```

---

## 📄 ARCHIVO 4: index.html

**Ubicación:** `/index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes" />
  
  <title>LANXESS - Protección Auditiva | Experiencia Inmersiva Educativa</title>
  <meta name="description" content="Aprende sobre protección auditiva con una experiencia inmersiva 3D. Mide decibeles en tiempo real." />
  
  <meta name="theme-color" content="#4CAF50" />
  <meta name="mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  
  <link rel="manifest" href="/manifest.json" />
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
  
  <link rel="preload" href="/Sonidos_De_Fabrica.wav" as="audio" type="audio/wav" />
  <link rel="preload" href="/microsoft_headphones_surface_2-v1.glb" as="fetch" type="model/gltf-binary" crossorigin />
  
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    html, body, #root { width: 100%; height: 100%; overflow-x: hidden; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
      background: linear-gradient(135deg, #0f0f1e 0%, #1a1a2e 100%);
      color: #ffffff;
    }
    
    #loading-screen {
      position: fixed; top: 0; left: 0; width: 100%; height: 100%;
      background: linear-gradient(135deg, #0f0f1e 0%, #1a1a2e 100%);
      display: flex; flex-direction: column; justify-content: center; align-items: center;
      z-index: 9999; transition: opacity 0.5s ease-out;
    }
    #loading-screen.hidden { opacity: 0; pointer-events: none; }
    
    .loader {
      width: 60px; height: 60px;
      border: 5px solid rgba(76, 175, 80, 0.2);
      border-top-color: #4CAF50;
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }
    @keyframes spin { to { transform: rotate(360deg); } }
    
    .loading-text {
      margin-top: 20px;
      color: #4CAF50;
      font-size: 16px;
      font-weight: 600;
    }
  </style>
</head>
<body>
  <noscript>
    <div style="position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); padding: 30px; background: rgba(244, 67, 54, 0.9); border-radius: 15px; color: white; text-align: center;">
      <h2>⚠️ JavaScript Requerido</h2>
      <p>Esta aplicación requiere JavaScript para funcionar.</p>
    </div>
  </noscript>
  
  <div id="loading-screen">
    <div style="font-size: 80px; margin-bottom: 20px;">🎧</div>
    <div class="loader"></div>
    <div class="loading-text">Cargando LANXESS...</div>
  </div>
  
  <div id="root"></div>
  
  <script>
    window.addEventListener('load', () => {
      setTimeout(() => {
        const loadingScreen = document.getElementById('loading-screen');
        if (loadingScreen) {
          loadingScreen.classList.add('hidden');
          setTimeout(() => loadingScreen.remove(), 500);
        }
      }, 1000);
    });
  </script>
  
  <script type="module" src="/src/main.jsx"></script>
</body>
</html>
```

---

## 📄 ARCHIVO 5: public/manifest.json

**Ubicación:** `/public/manifest.json`

```json
{
  "name": "LANXESS - Protección Auditiva",
  "short_name": "LANXESS Audio",
  "description": "Experiencia inmersiva educativa sobre protección auditiva",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#0f0f1e",
  "theme_color": "#4CAF50",
  "orientation": "portrait-primary",
  "scope": "/",
  "lang": "es-AR",
  "icons": [
    {
      "src": "/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any maskable"
    },
    {
      "src": "/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ]
}
```

---

## 📄 ARCHIVO 6: public/sw.js (Service Worker)

**Ubicación:** `/public/sw.js`

VER EN EL ARCHIVO QUE YA CREAMOS ANTERIORMENTE (muy largo para incluir aquí)

---

## 💻 CONTINÚA EN EL SIGUIENTE MENSAJE

Debido al límite de caracteres, continuaré con TODOS los archivos de React en el siguiente mensaje.

**ESCRIBE "CONTINÚA" PARA VER:**
- ✅ src/main.jsx
- ✅ src/App.jsx  
- ✅ src/index.css
- ✅ TODOS los componentes (7 archivos)
- ✅ Instrucciones de deployment
- ✅ Tips y troubleshooting