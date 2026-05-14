# 🎮 Pokémon AR — WebAR con MindAR + Three.js

Experiencia de Realidad Aumentada basada en imagen (image tracking).
- **PC**: Muestra imagen marcador como póster interactivo.
- **Celular**: Activa cámara AR con video + capas parallax 3D.

---

## 📁 Estructura de archivos

```
pokemon-ar/
├── index.html          ← Página principal (PC + móvil)
├── style.css           ← Estilos
├── script.js           ← Lógica AR (MindAR + Three.js)
├── vercel.json         ← Config de despliegue
└── assets/
    ├── targets.mind    ← Archivo de tracking (VER PASO 1)
    ├── marker.png      ← Imagen marcador que se muestra en PC
    ├── video.mp4       ← Video vertical Pokémon (VER PROMPTS)
    ├── background.png  ← Capa de fondo (más lejana)
    ├── middle.png      ← Capa media (personajes/energía)
    └── foreground.png  ← Capa delantera (más cercana)
```

---

## 🚀 Despliegue en 3 pasos

### Paso 1 — Genera el archivo targets.mind

1. Ve a: **https://hiukim.github.io/mind-ar-js-doc/tools/compile**
2. Sube `assets/marker.png`
3. Haz clic en **"Start"** y descarga el `targets.mind`
4. Colócalo en la carpeta `assets/`

### Paso 2 — Sube a GitHub

```bash
git init
git add .
git commit -m "Pokemon AR - initial"
git remote add origin https://github.com/TU-USUARIO/pokemon-ar.git
git push -u origin main
```

### Paso 3 — Despliega en Vercel

1. Ve a **vercel.com** → New Project
2. Importa el repositorio de GitHub
3. **Sin cambiar nada** → Deploy
4. ✅ Listo — Vercel genera una URL HTTPS automáticamente

---

## 🎨 Prompts para generar assets con IA

### 🖼️ MARKER IMAGE (Midjourney / Stable Diffusion / DALL·E)

```
Vertical Pokémon collectible poster card, 600x900px, ultra high contrast design optimized 
for image tracking / QR code style. Bold geometric patterns, thick black outlines, 
Pokéball centered in large format, golden decorative border frame with art nouveau flourishes. 
Dark midnight blue background (#0a0820). Charizard silhouette or Lugia legendary Pokémon 
featured prominently. High contrast black and white patterns in corners for AR tracking 
accuracy. "LEGENDARY EDITION" text in bold gold lettering. Style: official Nintendo trading 
card meets cinematic movie poster. No blur, maximum sharpness, clean edges.
Aspect ratio 2:3, PNG format.
```

> ⚠️ IMPORTANTE para el tracking: La imagen marcador DEBE tener:
> - Alto contraste (bordes oscuros sobre claro o viceversa)
> - Patrones no simétricos (no cuadros perfectos)
> - Bordes definidos
> - NO gradientes suaves sin detalles

---

### 🎬 VIDEO PRINCIPAL vertical (RunwayML / Pika Labs / Sora)

```
Cinematic vertical video 9:16, 1080x1920px, 12 seconds.
Scene: Lugia or Ho-Oh legendary Pokémon rising dramatically from a stormy ocean/volcano.
Epic lightning strikes illuminate the sky. Slow motion wings spreading wide.
Camera angle: low angle looking up at the Pokémon, heroic perspective.
Color palette: deep purples, electric blues, golden energy auras.
Visual style: Nintendo game cutscene meets Hollywood blockbuster.
No text, no UI. Pure cinematic moment.
Loop-friendly ending (fades to dramatic pose).
Format: MP4 H.264, 1080x1920, 30fps, max 15MB.
```

---

### 🌄 BACKGROUND.PNG (capa de fondo)

```
Digital painting, vertical 1080x1920px, PNG with full opacity.
Epic fantasy landscape for Pokémon AR background layer.
Night sky with aurora borealis in purple and blue tones.
Distant mountains silhouetted in deep indigo. Single large moon glowing.
Dozens of tiny stars scattered across sky.
Bottom third: dark alien grass field, bioluminescent green dots.
Color palette: #0a0820 to #1e0a4a gradient sky, #001020 ground.
Style: Studio Ghibli meets Pokémon anime background art.
NO characters. Pure environment. Soft painterly quality.
```

---

### 👾 MIDDLE.PNG (capa media — personajes/energía)

```
Vertical 1080x1920px PNG with TRANSPARENT BACKGROUND (alpha channel).
Central subject: Lugia or Suicune legendary Pokémon in heroic pose, center frame.
Surrounded by swirling energy auras, electric sparks, glowing rings.
Pokemon partially transparent/translucent body, ethereal appearance.
Energy beams radiating outward from center in all directions.
Floating light orbs around the character. 
Style: anime cel shading meets particle VFX.
CRITICAL: Background must be 100% transparent (checkerboard pattern in editor).
Only keep: Pokémon character + energy effects. Remove all sky/ground.
Export as PNG-24 with alpha channel preserved.
```

---

### ✨ FOREGROUND.PNG (capa delantera más cercana)

```
Vertical 1080x1920px PNG with TRANSPARENT BACKGROUND (alpha channel required).
ONLY the following elements, everything else transparent:
- Tall wild grass blades left and right edges of frame, dark green
- 6-8 large glowing sparkle stars scattered throughout (gold/white)
- Small Pokéball fragments floating in corners
- Energy streak particles (thin diagonal light streaks)
- Light blue rain-like particle effects falling diagonally
- Vignette darkness on far left and right edges
NO background. NO sky. NO characters. ONLY overlay elements.
The center 60% of the image should be 100% transparent.
PNG-24 with alpha, no white border artifacts.
```

---

## 📐 Especificaciones técnicas

| Asset | Tamaño | Formato | Notas |
|-------|--------|---------|-------|
| marker.png | 600×900 | PNG RGB | Alto contraste obligatorio |
| targets.mind | — | .mind | Generado desde marker.png |
| video.mp4 | 1080×1920 | MP4 H.264 | Max 15MB, loop |
| background.png | 1080×1920 | PNG RGBA | Opaco está bien |
| middle.png | 1080×1920 | PNG RGBA | **Alpha channel obligatorio** |
| foreground.png | 1080×1920 | PNG RGBA | **Alpha channel obligatorio** |

---

## 🧪 Testing local (opcional)

```bash
# Con Python
python3 -m http.server 8080
# Abrir en móvil: http://[TU-IP-LOCAL]:8080
# ⚠️ El tracking AR SOLO funciona en HTTPS o localhost
```

---

## 🔧 Troubleshooting

| Problema | Solución |
|----------|----------|
| "targets.mind not found" | Genera el .mind desde hiukim.github.io/mind-ar-js-doc/tools/compile |
| Video no reproduce | Verifica que sea MP4 H.264, muted, y menor a 15MB |
| No detecta el marcador | La imagen marcador necesita más contraste y detalle único |
| Error de cámara en iOS | Safari Settings → Camera → Allow para el dominio |
| Capas con borde blanco | Re-exportar PNG con "Save for Web" preservando alpha |
