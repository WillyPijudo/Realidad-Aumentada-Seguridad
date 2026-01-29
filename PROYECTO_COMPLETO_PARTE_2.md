# 🎧 LANXESS - PARTE 2: COMPONENTES REACT

## 📄 ARCHIVO 7: src/main.jsx

**Ubicación:** `/src/main.jsx`

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

// Registro del Service Worker para PWA
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/sw.js').then(
      (registration) => {
        console.log('✅ Service Worker registrado:', registration.scope)
      },
      (error) => {
        console.log('❌ Error al registrar Service Worker:', error)
      }
    )
  })
}

// Soporte para instalación de PWA
let deferredPrompt
window.addEventListener('beforeinstallprompt', (e) => {
  e.preventDefault()
  deferredPrompt = e
  window.deferredPrompt = deferredPrompt
})

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

---

## 📄 ARCHIVO 8: src/App.jsx (COMPONENTE PRINCIPAL - MUY IMPORTANTE)

**Ubicación:** `/src/App.jsx`

**⚠️ ESTE ES EL ARCHIVO MÁS IMPORTANTE - MANEJA TODO EL FLUJO**

VER EL ARCHIVO `AppNUEVO.jsx` QUE YA CREAMOS (código completo con toda la lógica)

**RESUMEN DEL ARCHIVO:**
- Maneja navegación entre pantallas
- Estados globales del usuario
- Sistema de logros
- Tracking de exposición
- LocalStorage para persistencia
- Control de progreso

**PANTALLAS QUE MANEJA:**
1. SPLASH → SplashScreen inicial
2. ONBOARDING → Tutorial interactivo
3. EXPERIENCIA → Simulación inmersiva
4. MENSAJE_FINAL → Educación sobre vida diaria
5. MEDIDOR_REAL → Herramienta de medición diaria

---

## 📄 ARCHIVO 9: src/index.css (ESTILOS GLOBALES)

**Ubicación:** `/src/index.css`

VER EL ARCHIVO `INDEX_CSS.css` QUE YA CREAMOS (estilos completos + variables CSS + responsive + PWA)

**INCLUYE:**
- Variables CSS para colores, espaciados, sombras
- Reset global y tipografía
- Animaciones personalizadas (pulse, shake, glow, fadeIn)
- Glass morphism effects
- Scrollbar personalizado
- Responsive design (mobile, tablet, desktop)
- Modo reducido de movimiento (accesibilidad)
- Estilos para PWA

---

## 📄 ARCHIVO 10: src/components/SplashScreen.jsx

**Ubicación:** `/src/components/SplashScreen.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**CARACTERÍSTICAS:**
- Logo animado con partículas de fondo
- Barra de progreso (0-100%)
- Animaciones con Framer Motion
- Transición automática al onboarding

---

## 📄 ARCHIVO 11: src/components/Onboarding.jsx (TUTORIAL)

**Ubicación:** `/src/components/Onboarding.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**5 PASOS DEL TUTORIAL:**
1. Bienvenida con intro
2. Explicación de funcionalidades
3. Solicitud de permiso de micrófono
4. Input de nombre personalizado
5. Tips finales antes de comenzar

**CARACTERÍSTICAS:**
- Validación de permisos
- Input personalizado de nombre
- Indicador de progreso
- Navegación adelante/atrás
- Animaciones fluidas

---

## 📄 ARCHIVO 12: src/components/ExperienciaInmersiva.jsx (CORAZÓN DEL PROYECTO)

**Ubicación:** `/src/components/ExperienciaInmersiva.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**⭐ COMPONENTE MÁS IMPORTANTE ⭐**

**7 FASES DE LA EXPERIENCIA:**
1. Introducción
2. Ambiente silencioso (50 dB)
3. Ruido moderado (70 dB)
4. ZONA DE PELIGRO sin protección (105 dB) ⚠️
5. Colocando protección auditiva
6. Protegido CON auriculares (70 dB) ✅
7. Comparación final

**CARACTERÍSTICAS CLAVE:**
- ✅ Modelo 3D de auriculares rotando (Three.js)
- ✅ Sonido de fábrica con volumen variable
- ✅ Medidor de decibeles simulado en tiempo real
- ✅ Partículas 3D de sonido
- ✅ Sistema de fases automático
- ✅ Botón para poner/quitar auriculares
- ✅ Alertas visuales en zona de peligro
- ✅ Tracking de exposición

**RUTAS DE ARCHIVOS IMPORTANTES:**
- Audio: `/Sonidos_De_Fabrica.wav`
- Modelo 3D: `/microsoft_headphones_surface_2-v1.glb`

**CÓMO FUNCIONA EL SONIDO:**
1. Se carga el archivo WAV al inicio
2. Volumen se ajusta según decibeles simulados
3. Si pones auriculares → volumen baja 70%
4. Loop infinito mientras dure la experiencia

**CÓMO FUNCIONA EL MEDIDOR:**
- Decibeles se interpolan suavemente hacia el objetivo
- Cada fase tiene un `decibelesObjetivo`
- Color cambia según nivel:
  - Verde < 60 dB (Seguro)
  - Azul < 85 dB (Normal)
  - Naranja < 95 dB (Atención)
  - Rojo ≥ 95 dB (Peligro)

---

## 📄 ARCHIVO 13: src/components/MensajeFinal.jsx (EDUCACIÓN)

**Ubicación:** `/src/components/MensajeFinal.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**SECCIONES:**
1. ✅ Felicitaciones con confetti
2. 💡 Mensaje educativo principal
3. 🌍 6 Situaciones cotidianas de riesgo:
   - Tráfico pesado (85 dB)
   - Conciertos (110 dB)
   - Herramientas eléctricas (100 dB)
   - Audífonos a volumen alto (95 dB)
   - Avión despegando (120 dB)
   - Motocicleta (90 dB)
4. 📊 Estadísticas del usuario
5. 🚀 Llamada a la acción

**CADA SITUACIÓN INCLUYE:**
- Icono emoji
- Nivel de decibeles
- Tiempo de exposición segura
- Nivel de riesgo (código de color)
- Consejo específico

---

## 📄 ARCHIVO 14: src/components/MedidorReal.jsx (HERRAMIENTA DIARIA)

**Ubicación:** `/src/components/MedidorReal.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**⭐ SEGUNDO COMPONENTE MÁS IMPORTANTE ⭐**

**CARACTERÍSTICAS:**
- ✅ Usa el micrófono REAL del dispositivo
- ✅ Web Audio API para análisis de frecuencias
- ✅ Cálculo de RMS → conversión a dB
- ✅ Medición en tiempo real (actualización cada 100ms)
- ✅ Estadísticas: Promedio, Máximo, Tiempo
- ✅ Alertas cuando > 85 dB
- ✅ Historial de mediciones guardado
- ✅ Calibración manual (±20 dB)
- ✅ Recomendaciones según nivel

**CÓMO FUNCIONA:**
1. Usuario presiona "INICIAR MEDICIÓN"
2. Solicita permiso de micrófono
3. Crea AudioContext y Analyser
4. Conecta micrófono → analyser
5. Loop de animación lee frecuencias
6. Calcula RMS de las frecuencias
7. Convierte a decibeles: `dB = 20 * log10(RMS)`
8. Actualiza UI en tiempo real
9. Guarda en historial al detener

**FÓRMULA DE DECIBELES:**
```javascript
const calcularDecibeles = (dataArray) => {
  let suma = 0
  for (let i = 0; i < dataArray.length; i++) {
    suma += dataArray[i] * dataArray[i]
  }
  const rms = Math.sqrt(suma / dataArray.length)
  let db = 20 * Math.log10(rms + 1)
  db = Math.max(30, Math.min(120, db + 30 + calibracion))
  return Math.round(db)
}
```

**NIVELES DE RIESGO:**
- < 60 dB → SEGURO ✅ (Verde)
- < 75 dB → NORMAL ℹ️ (Azul)
- < 85 dB → ATENCIÓN ⚠️ (Naranja)
- < 100 dB → PELIGRO 🚨 (Rojo)
- ≥ 100 dB → CRÍTICO ☢️ (Morado)

---

## 📄 ARCHIVO 15: src/components/Navegacion.jsx

**Ubicación:** `/src/components/Navegacion.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**CARACTERÍSTICAS:**
- Barra superior fija con logo LANXESS
- Barra de progreso global (0-100%)
- Menú desplegable para navegar
- Panel de estadísticas
- Responsive y glass morphism

---

## 📄 ARCHIVO 16: src/components/InstallPrompt.jsx

**Ubicación:** `/src/components/InstallPrompt.jsx`

VER EL ARCHIVO QUE YA CREAMOS

**CARACTERÍSTICAS:**
- Detecta cuando la PWA puede instalarse
- Prompt automático después de 10 segundos
- Instrucciones específicas para iOS
- Botones: Instalar / Después / Cerrar
- Se oculta si el usuario rechaza

---

## 🚀 DEPLOYMENT EN NETLIFY

### PASO 1: Preparar el Proyecto

```bash
# Asegúrate de tener todos los archivos
npm run build

# Verifica que la carpeta dist/ se creó correctamente
ls dist/
```

### PASO 2: Subir a GitHub (Recomendado)

```bash
git init
git add .
git commit -m "Initial commit - LANXESS PWA"
git remote add origin TU_URL_DE_GITHUB
git push -u origin main
```

### PASO 3: Deploy en Netlify

**Opción A: Desde Git (Automático)**
1. Ve a [netlify.com](https://netlify.com)
2. "Add new site" → "Import an existing project"
3. Conecta GitHub
4. Selecciona tu repo
5. Settings automáticos (Vite detectado):
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Node version: 18
6. Deploy!

**Opción B: Manual (Drag & Drop)**
1. `npm run build` localmente
2. Arrastra carpeta `dist/` a Netlify
3. ¡Listo!

### PASO 4: Generar QR Code

```bash
# Tu URL de Netlify
https://tu-proyecto.netlify.app

# Ve a qr-code-generator.com
# Pega tu URL
# Descarga el QR en alta calidad
# Imprímelo para las cartas
```

---

## 🎨 PERSONALIZACIÓN RÁPIDA

### Cambiar Colores

**Archivo:** `src/index.css`

```css
:root {
  --color-primary: #4CAF50;  /* CAMBIAR AQUÍ */
}
```

### Cambiar Textos

**Archivo:** `src/components/MensajeFinal.jsx`

Busca el array `situacionesCotidianas` y edita.

### Agregar Logo

**Archivo:** `src/components/SplashScreen.jsx`

```jsx
<img src="/logo-empresa.png" alt="Logo" />
```

---

## 🐛 TROUBLESHOOTING

### ❌ Error: "Cannot find module 'three'"

**Solución:**
```bash
rm -rf node_modules package-lock.json
npm install
```

### ❌ Sonido no se reproduce

**Causa:** Autoplay bloqueado por navegador

**Solución:** Ya implementada - requiere interacción del usuario (botón "Iniciar")

**Verifica:**
- Archivo `Sonidos_De_Fabrica.wav` está en `public/`
- No hay errores en consola (F12)

### ❌ Modelo 3D no aparece

**Verifica:**
- `microsoft_headphones_surface_2-v1.glb` está en `public/`
- El archivo no está corrupto
- Prueba el modelo en [gltf-viewer.donmccurdy.com](https://gltf-viewer.donmccurdy.com/)

### ❌ Micrófono no funciona

**Causas posibles:**
- Sin HTTPS (usa Netlify)
- Permisos denegados
- Otro programa usando el micrófono

**Solución:**
- Netlify provee HTTPS automático
- Revisa permisos del navegador
- Cierra otras apps que usen micrófono

### ❌ PWA no se instala

**Verifica:**
- Todos los iconos existen en `public/`
- `manifest.json` está correcto
- Service Worker sin errores (F12 → Application)
- Estás usando HTTPS

---

## 📦 ARCHIVOS QUE DEBES CONSEGUIR

### ✅ Ya Tienes:
- `Sonidos_De_Fabrica.wav`
- `microsoft_headphones_surface_2-v1.glb`

### ❌ Necesitas Crear:

**ICONOS PWA (usa [RealFaviconGenerator.net](https://realfavicongenerator.net/)):**
```
/public/
  ├── favicon.ico
  ├── favicon-16x16.png
  ├── favicon-32x32.png
  ├── icon-72x72.png
  ├── icon-96x96.png
  ├── icon-128x128.png
  ├── icon-144x144.png
  ├── icon-152x152.png
  ├── icon-192x192.png
  ├── icon-384x384.png
  ├── icon-512x512.png
  └── apple-touch-icon.png (180x180)
```

**CÓMO CREAR ICONOS:**
1. Diseña un logo 512x512px (usa Canva gratis)
2. Sube a [RealFaviconGenerator.net](https://realfavicongenerator.net/)
3. Genera todos los tamaños
4. Descarga el .zip
5. Copia todo a `public/`

**ALTERNATIVA RÁPIDA:**
Usa un emoji como icono temporal:
```bash
# Busca "headphone emoji png 512x512" en Google
# Descarga y renombra como icon-512x512.png
```

---

## ✅ CHECKLIST FINAL ANTES DE PRESENTAR

```
[ ] npm install ejecutado sin errores
[ ] npm run dev funciona localmente
[ ] Sonidos_De_Fabrica.wav en public/
[ ] microsoft_headphones_surface_2-v1.glb en public/
[ ] Iconos PWA creados (al menos icon-192 y icon-512)
[ ] npm run build sin errores
[ ] Deploy en Netlify exitoso
[ ] HTTPS activo (automático en Netlify)
[ ] PWA instalable en móvil
[ ] Micrófono funciona en dispositivo real
[ ] Modelo 3D carga correctamente
[ ] Sonidos se reproducen
[ ] QR code generado
[ ] Probado en Chrome mobile
[ ] Probado en Safari iOS
```

---

## 🎉 ¡LISTO PARA IMPRESIONAR!

Tu app estará en:
```
https://nombre-proyecto.netlify.app
```

**Tips para la demo:**
1. Carga la app antes de presentar
2. Ten WiFi estable
3. Prueba el micrófono antes
4. Muestra el QR impreso
5. Explica las 3 partes:
   - Experiencia inmersiva educativa
   - Mensaje sobre vida diaria
   - Herramienta de medición real

---

**¿DUDAS O ERRORES?**
Revisa la consola del navegador (F12) - ahí aparecen todos los errores con explicación.

¡Mucha suerte! 🚀🎧💚
