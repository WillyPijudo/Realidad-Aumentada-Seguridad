# 🎧 GUÍA RÁPIDA DE IMPLEMENTACIÓN - LANXESS PWA

## ⚡ INICIO RÁPIDO (5 MINUTOS)

### 1. Crear proyecto base
```bash
npm create vite@latest lanxess-proteccion-auditiva -- --template react
cd lanxess-proteccion-auditiva
npm install
```

### 2. Instalar dependencias adicionales
```bash
npm install three @react-three/fiber @react-three/drei framer-motion zustand react-confetti howler
npm install -D vite-plugin-pwa
```

### 3. Reemplazar archivos

**⚠️ IMPORTANTE - RENOMBRAR PRIMERO:**
- `PACKAGE.json` → `package.json`
- `INDEX_HTML.html` → `index.html`  
- `AppNUEVO.jsx` → `App.jsx`
- `INDEX_CSS.css` → `index.css`

```bash
# Reemplaza estos archivos con los que descargaste:
package.json
vite.config.js
netlify.toml
index.html
src/main.jsx
src/App.jsx
src/index.css

# Copia la carpeta components/ completa
src/components/
```

### 4. Agregar tus assets
```bash
# Copia a public/:
public/Sonidos_De_Fabrica.wav
public/microsoft_headphones_surface_2-v1.glb
public/manifest.json
public/sw.js
public/icon-192x192.png
public/icon-512x512.png
```

### 5. Probar
```bash
npm run dev
```

### 6. Build y Deploy
```bash
npm run build
# Arrastra carpeta dist/ a netlify.com
```

---

## 📋 ARCHIVOS QUE TIENES

✅ **PROYECTO_COMPLETO_PARTE_1.md** - Setup y configuración
✅ **PROYECTO_COMPLETO_PARTE_2.md** - Componentes React  
✅ **GUIA_RAPIDA.md** - Este archivo
✅ Todos los archivos .jsx, .js, .json necesarios

---

## 🔥 TROUBLESHOOTING RÁPIDO

**Error: "Module not found"**
```bash
rm -rf node_modules package-lock.json && npm install
```

**Sonido no se reproduce**
- Verifica que `Sonidos_De_Fabrica.wav` esté en `public/`

**Modelo 3D no aparece**
- Verifica que `microsoft_headphones_surface_2-v1.glb` esté en `public/`

**Micrófono no funciona**
- Usa HTTPS (Netlify lo da automático)
- Otorga permisos cuando el navegador pregunte

---

## ✅ CHECKLIST PRE-PRESENTACIÓN

```
[ ] npm run dev funciona sin errores
[ ] Sonidos_De_Fabrica.wav en public/
[ ] microsoft_headphones_surface_2-v1.glb en public/
[ ] Iconos creados (mínimo 192 y 512)
[ ] Build exitoso (npm run build)
[ ] Deploy en Netlify hecho
[ ] QR code generado
[ ] Probado en móvil real
```

---

¡MUCHA SUERTE! 🚀
