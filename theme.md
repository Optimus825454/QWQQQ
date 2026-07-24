# Cyberpunk Neon Theme Guide

Tasarım sistemi, renk paleti, animasyonlar ve Three.js arka plan kurulumu.

---

## 1. Renk Paleti (CSS Custom Properties)

```css
:root {
  /* Ana Renkler */
  --primary: #2563eb;
  --primary-dark: #1d4ed8;
  --secondary: #7c3aed;
  --accent: #06b6d4;

  /* Durum Renkleri */
  --success: #10b981;
  --warning: #f59e0b;
  --danger: #ef4444;

  /* Nötr Renkler */
  --dark: #0f172a;
  --dark-light: #1e293b;
  --gray: #64748b;
  --gray-light: #94a3b8;
  --light: #f1f5f9;
  --white: #fff;

  /* Neon Renkler - Ana tema renkleri */
  --neon-cyan: #00f5ff;
  --neon-magenta: #ff00ff;
  --neon-green: #00ff88;
  --neon-gold: #ffd700;

  /* Gradyanlar */
  --gradient-1: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  --gradient-2: linear-gradient(135deg, #2563eb 0%, #7c3aed 100%);
  --gradient-3: linear-gradient(135deg, #06b6d4 0%, #10b981 100%);
  --gradient-neon: linear-gradient(135deg, #00f5ff 0%, #ff00ff 100%);
  --gradient-green: linear-gradient(135deg, #00f5ff 0%, #00ff88 100%);

  /* Gölge */
  --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 25px 50px -12px rgba(0, 0, 0, 0.25);

  /* Border Radius */
  --radius: 12px;
  --radius-lg: 20px;
}
```

---

## 2. Font

```html
<link
  href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap"
  rel="stylesheet"
/>
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
/>
```

```css
body {
  font-family: "Plus Jakarta Sans", sans-serif;
}
```

---

## 3. Sayfa Temel Yapısı

```css
body {
  font-family: "Plus Jakarta Sans", sans-serif;
  color: #e0e0e0;
  line-height: 1.6;
  overflow-x: hidden;
  background: #0a0a0f; /* Koyu cyberpunk zemin */
}

/* Three.js canvas - sayfanın arkasında */
#three-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

/* Tarama çizgileri efekti */
.scanlines {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
  background: repeating-linear-gradient(
    0deg,
    rgba(0, 0, 0, 0.1),
    rgba(0, 0, 0, 0.1) 1px,
    transparent 1px,
    transparent 2px
  );
  opacity: 0.2;
}

/* İçerik katmanı */
.page-content {
  position: relative;
  z-index: 10;
}

section {
  background: transparent !important; /* Three.js arka planı görünsün */
}
```

---

## 4. Glass Morphism Efektleri

```css
/* Temel glass */
.glass {
  background: rgba(10, 10, 15, 0.7);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(0, 245, 255, 0.1);
}

/* Section glass - daha koyu */
.section-glass {
  background: rgba(10, 10, 15, 0.75);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border-radius: var(--radius-lg);
  padding: 40px;
  border: 1px solid rgba(0, 245, 255, 0.1);
}
```

---

## 5. Neon Glow Efektleri

```css
/* Metin glow */
.neon-glow-cyan {
  text-shadow:
    0 0 10px #00f5ff,
    0 0 20px #00f5ff,
    0 0 40px #00f5ff;
}

.neon-glow-magenta {
  text-shadow:
    0 0 10px #ff00ff,
    0 0 20px #ff00ff,
    0 0 40px #ff00ff;
}

/* Gradyan metin */
.gradient-text {
  background: linear-gradient(135deg, #00f5ff 0%, #ff00ff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## 6. Buton Stilleri

```css
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  border-radius: var(--radius);
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  border: none;
  cursor: pointer;
  font-size: 0.95rem;
}

.btn-primary {
  background: linear-gradient(135deg, #00f5ff 0%, #7c3aed 100%);
  color: #0a0a0f;
  box-shadow: 0 4px 14px rgba(0, 245, 255, 0.4);
  font-weight: 700;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 245, 255, 0.6);
}

.btn-outline {
  background: transparent;
  color: var(--neon-cyan);
  border: 2px solid var(--neon-cyan);
}

.btn-outline:hover {
  background: var(--neon-cyan);
  color: #0a0a0f;
  box-shadow: 0 0 20px rgba(0, 245, 255, 0.5);
}
```

---

## 7. Animasyonlar

### 7a. Tarama Çizgisi (QR Kod Tarayıcı)

```css
.qr-scan-line {
  position: absolute;
  left: 10%;
  right: 10%;
  height: 3px;
  background: var(--success);
  top: 50%;
  animation: scan 2s ease-in-out infinite;
  box-shadow: 0 0 10px var(--success);
}

@keyframes scan {
  0%,
  100% {
    top: 20%;
    opacity: 1;
  }
  50% {
    top: 80%;
    opacity: 0.5;
  }
}
```

### 7b. Pulse (AI Beyin Dalgalanması)

```css
.ai-pulse {
  position: absolute;
  inset: 0;
  border-radius: 50%;
  border: 2px solid var(--neon-cyan);
  animation: pulse 2s ease-out infinite;
}

.ai-pulse.pulse-2 {
  animation-delay: 0.5s;
  border-color: var(--neon-magenta);
}

.ai-pulse.pulse-3 {
  animation-delay: 1s;
}

@keyframes pulse {
  0% {
    transform: scale(1);
    opacity: 0.8;
  }
  100% {
    transform: scale(2.5);
    opacity: 0;
  }
}
```

### 7c. Glow (AI İkon Parlaması)

```css
.task-step-icon.ai-glow {
  animation: glow 2s ease-in-out infinite;
}

@keyframes glow {
  0%,
  100% {
    filter: drop-shadow(0 0 5px rgba(0, 245, 255, 0.5));
  }
  50% {
    filter: drop-shadow(0 0 20px rgba(0, 245, 255, 0.8));
  }
}
```

### 7d. Scroll Animasyonları (Intersection Observer)

```javascript
// Elementleri kaydırırken fade-in + slide-up yapar
const observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.style.opacity = "1";
        entry.target.style.transform = "translateY(0)";
      }
    });
  },
  { threshold: 0.1, rootMargin: "0px 0px -50px 0px" },
);

document
  .querySelectorAll(
    ".feature-card, .benefit-card, .ai-card, .panel-showcase, .task-step, .qr-path, .tech-card",
  )
  .forEach((el) => {
    el.style.opacity = "0";
    el.style.transform = "translateY(30px)";
    el.style.transition = "opacity 0.6s ease, transform 0.6s ease";
    observer.observe(el);
  });
```

### 7e. Hover Efektleri (Kartlar)

```css
/* Kart hover: yukarı kaydırma + neon glow */
.feature-card:hover,
.tech-card:hover,
.benefit-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 0 30px rgba(0, 245, 255, 0.3);
  border-color: rgba(0, 245, 255, 0.3);
}

/* Navbar scroll: cam efekti */
.navbar.scrolled {
  background: rgba(10, 10, 15, 0.9);
  backdrop-filter: blur(10px);
  box-shadow: 0 0 20px rgba(0, 245, 255, 0.2);
  border-bottom: 1px solid rgba(0, 245, 255, 0.1);
}
```

---

## 8. Three.js Arka Plan (Cyberpunk Particle System)

### 8a. Kurulum

```html
<canvas id="three-canvas"></canvas>
<div class="scanlines"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
```

### 8b. Sistem Yapısı

| Öğe               | Açıklama         | Değer                                 |
| ----------------- | ---------------- | ------------------------------------- |
| Sahne             | Three.js sahnesi | `alpha: true, antialias: true`        |
| Kamera            | Perspektif       | FOV: 75, Near: 0.1, Far: 1000         |
| Parçacık          | Sayı             | 2500                                  |
| Parçacık Renk     | Cyan             | `0x00f5ff`                            |
| Parçacık Boyutu   | Nokta            | `0.015`                               |
| Parçacık Yayılımı | Alan             | `(-6, 6)` x, y, z                     |
| Karışım           | Additive         | `THREE.AdditiveBlending`              |
| Geometri          | Şekiller         | Icosahedron, Octahedron, Tetrahedron  |
| Şekil Sayısı      | 3 boyutlu        | 20 adet                               |
| Şekil Renk        | Karışık          | `0x00f5ff` (cyan) ve `0x7c3aed` (mor) |

### 8c. Animasyon Döngüsü

```javascript
// Parçacık dönüşü - sabit hız + mouse etkisi
particlesMesh.rotation.y = elapsedTime * 0.03;
particlesMesh.rotation.x = targetY * 0.2;
particlesMesh.rotation.y += targetX * 0.2;

// Şekiller - kendi ekseni etrafında dönme + dikey süzülme
shapes.forEach((shape) => {
  shape.rotation.x += shape.userData.rotationSpeed.x; // rastgele: -0.0075 ~ 0.0075
  shape.rotation.y += shape.userData.rotationSpeed.y;
  shape.rotation.z += shape.userData.rotationSpeed.z;
  shape.position.y +=
    Math.sin(
      elapsedTime * shape.userData.floatSpeed + shape.userData.floatOffset,
    ) * 0.002;
});

// Kamera - mouse takibi (yumuşak geçiş)
camera.position.x += (targetX * 0.4 - camera.position.x) * 0.02;
camera.position.y += (targetY * 0.4 - camera.position.y) * 0.02;
```

### 8d. Mouse Etkileşimi

```javascript
let mouseX = 0,
  mouseY = 0;
let targetX = 0,
  targetY = 0;

document.addEventListener("mousemove", (event) => {
  mouseX = (event.clientX / window.innerWidth) * 2 - 1; // -1 ~ 1
  mouseY = -(event.clientY / window.innerHeight) * 2 + 1; // -1 ~ 1
});

// yumuşatma katsayısı
targetX += (mouseX - targetX) * 0.05;
targetY += (mouseY - targetY) * 0.05;
```

### 8e. Scroll Paralaksı

```javascript
window.addEventListener("scroll", () => {
  const scrolled = window.pageYOffset;
  particlesMesh.position.y = scrolled * 0.0008; // çok hafif yukarı kaydırma
});
```

### 8f. Pencere Yeniden Boyutlandırma

```javascript
window.addEventListener("resize", () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});
```

---

## 9. Kart & Bileşen Stilleri

### 9a. Glass Kart (Genel Kullanım)

```css
.glass-card {
  background: rgba(10, 10, 15, 0.7);
  border-radius: var(--radius-lg);
  padding: 30px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  transition:
    transform 0.3s,
    box-shadow 0.3s;
}

.glass-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 0 30px rgba(0, 245, 255, 0.3);
  border-color: rgba(0, 245, 255, 0.3);
}
```

### 9b. Neon Border Kart

```css
.neon-card {
  background: rgba(10, 10, 15, 0.7);
  border-radius: var(--radius);
  padding: 24px;
  border: 1px solid rgba(0, 245, 255, 0.2);
  backdrop-filter: blur(10px);
}

.neon-card:hover {
  border-color: rgba(0, 245, 255, 0.4);
  box-shadow: 0 0 20px rgba(0, 245, 255, 0.2);
}
```

### 9c. Gradyan İkon Kutusu

```css
.icon-box {
  width: 60px;
  height: 60px;
  border-radius: var(--radius);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  color: #fff;
}

.icon-box.cyan-magenta {
  background: linear-gradient(135deg, #00f5ff 0%, #7c3aed 100%);
}

.icon-box.magenta-cyan {
  background: linear-gradient(135deg, #ff00ff 0%, #00f5ff 100%);
}

.icon-box.cyan-green {
  background: linear-gradient(135deg, #00f5ff 0%, #00ff88 100%);
}
```

### 9d. Neon Badge

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(0, 245, 255, 0.15);
  color: var(--neon-cyan);
  padding: 8px 16px;
  border-radius: 50px;
  font-weight: 600;
  font-size: 0.85rem;
  border: 1px solid rgba(0, 245, 255, 0.3);
}

.badge.magenta {
  background: rgba(255, 0, 255, 0.15);
  color: var(--neon-magenta);
  border-color: rgba(255, 0, 255, 0.3);
}

.badge.green {
  background: rgba(0, 255, 136, 0.15);
  color: var(--neon-green);
  border-color: rgba(0, 255, 136, 0.3);
}
```

---

## 10. Navbar

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 16px 0;
  transition: all 0.3s ease;
}

.navbar.scrolled {
  background: rgba(10, 10, 15, 0.9);
  backdrop-filter: blur(10px);
  box-shadow: 0 0 20px rgba(0, 245, 255, 0.2);
  border-bottom: 1px solid rgba(0, 245, 255, 0.1);
  padding: 12px 0;
}

.nav-links a {
  text-decoration: none;
  color: #e0e0e0;
  font-weight: 500;
  transition: all 0.3s;
}

.nav-links a:hover {
  color: var(--neon-cyan);
  text-shadow: 0 0 10px var(--neon-cyan);
}
```

---

## 11. Responsive Kırılma Noktaları

| Breakpoint | Cihaz                  |
| ---------- | ---------------------- |
| `1024px`   | Tablet (yatay)         |
| `768px`    | Tablet (dikey) / Mobil |
| `480px`    | Küçük Mobil            |

Mobilde:

- Nav linkleri gizlenir, hamburger menü açılır
- Gridler tek sütuna düşer
- `task-arrow` 90° döndürülür (dikey ok)
- Boyutlar %20-30 küçülür

---

## 12. Lightbox (Görsel Büyütme)

```css
.lightbox-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  backdrop-filter: blur(10px);
  z-index: 9999;
  display: none;
  align-items: center;
  justify-content: center;
  cursor: zoom-out;
}

.lightbox-overlay.active {
  display: flex;
  opacity: 1;
}

.lightbox-image {
  max-width: 95%;
  max-height: 95vh;
  border-radius: var(--radius);
  border: 2px solid rgba(0, 245, 255, 0.3);
  box-shadow: 0 0 60px rgba(0, 245, 255, 0.3);
}
```

---

## 13. Quick Start - Minimum Kurulum

Herhangi bir projeye bu temayı uygulamak için:

1. **HTML base** ekle (canvas + scanlines + page-content)
2. **CSS variable'ları** `:root` içine kopyala
3. **Three.js script'ini** kopyala
4. **Glass morphism** ve **neon glow** CSS'lerini ekle
5. **Font** olarak Plus Jakarta Sans kullan

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
    />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  </head>
  <body>
    <canvas id="three-canvas"></canvas>
    <div class="scanlines"></div>
    <div class="page-content">
      <!-- İçerik -->
    </div>
  </body>
</html>
```
