---
marp: true
theme: default
paginate: true
style: |
  section {
    background: #06060f;
    color: #f0f0ff;
    font-family: 'Nunito', 'Segoe UI', sans-serif;
  }
  h1, h2, h3 { color: #00e676; font-family: 'Bangers', 'Impact', cursive; letter-spacing: 2px; }
  h2 { color: #00cfff; }
  h3 { color: #ff4dff; }
  code { background: #10102a; color: #ffe135; border-radius: 4px; padding: 2px 6px; }
  pre { background: #10102a; border: 2px solid #1e1e4a; border-radius: 12px; padding: 16px; }
  pre code { color: #f0f0ff; }
  strong { color: #00e676; }
  em { color: #ffe135; font-style: normal; }
  table { border-collapse: collapse; width: 100%; }
  th { background: #1e1e4a; color: #00cfff; padding: 8px 12px; }
  td { padding: 8px 12px; border-bottom: 1px solid #1e1e4a; }
  blockquote { border-left: 4px solid #00e676; background: #10102a; padding: 12px 20px; margin: 16px 0; }
---

# 🛸 Weed World
## Agencia de Viajes Interdimensionales

Proyecto web en **HTML + CSS puro**  
Equipo: Boris · Jordi · Edgar · Roger

---

## 📁 Estructura del proyecto

```
weeder/
├── index.html        ← estructura y contenido
├── README.md         ← documentación
└── src/
    └── styles.css    ← toda la visual
```

> Un único archivo HTML + un único CSS.  
> **Sin frameworks. Sin dependencias. Sin magia oculta.**

---

## 🎨 Sistema de diseño — Variables CSS

El CSS arranca con un bloque `:root` que centraliza toda la paleta:

```css
:root {
  --portal-green:  #00e676;   /* verde neón del portal */
  --rick-blue:     #00cfff;
  --morty-yellow:  #ffe135;
  --alien-pink:    #ff4dff;
  --space-bg:      #06060f;   /* fondo negro espacial */
  --card-bg:       #10102a;

  --font-head: 'Bangers', cursive;   /* títulos estilo cómic */
  --font-body: 'Nunito', sans-serif;
}
```

Cambiar un color aquí lo actualiza en **toda la página** automáticamente.

---

## ⭐ Fondo de estrellas animado

El cielo estrellado es **CSS puro** — sin imágenes ni JS:

```css
.stars {
  position: fixed;
  inset: 0;
  background:
    radial-gradient(1px 1px at 10% 15%, #fff, transparent),
    radial-gradient(1.5px 1.5px at 55% 25%, #aef, transparent),
    radial-gradient(2px 2px at 90% 40%, #aef, transparent);
  animation: twinkle 4s infinite alternate;
}

@keyframes twinkle {
  0%   { opacity: 0.6; }
  100% { opacity: 1;   }
}
```

Dos capas (`.stars` + `.stars2`) con ritmos distintos crean **efecto de profundidad**.

---

## 🧭 Navbar — Boris

```css
.navbar {
  position: sticky;   /* se queda fija al hacer scroll */
  top: 0;
  z-index: 100;
  backdrop-filter: blur(12px);          /* cristal esmerilado */
  border-bottom: 3px solid #00e676;
  box-shadow: 0 0 20px rgba(0,230,118,0.3);
}
```

**Resultado visual:**

```
┌─────────────────────────────────────────────────────────┐
│ 🛸 WEED WORLD    Destinos  Sobre nosotros  Contacto     │
│                        "No vendemos viajes…"            │
└═════════════════════════ verde neón ════════════════════┘
         ↑ sticky · blur · halo verde bajo la barra
```

---

## 🚀 Hero — Boris

```html
<section class="hero">
  <div class="portal-ring" aria-hidden="true"></div>  <!-- anillo giratorio -->

  <div class="hero-content">
    <p class="hero-badge">👽 INTERDIMENSIONAL TRAVEL CO.</p>
    <h1 class="hero-title">Tu próxima realidad está a un clic</h1>
    <a href="#destinos" class="btn btn-hero">🚀 Explorar Destinos</a>
  </div>

  <div class="hero-alien" aria-hidden="true">...</div>  <!-- alien CSS puro -->
</section>
```

> `aria-hidden="true"` en los elementos decorativos: los lectores de pantalla los **ignoran**. Buena práctica de accesibilidad.

---

## 🌀 Portal y alienígena — CSS puro

```css
/* Anillo de colores giratorio */
.portal-ring {
  background: conic-gradient(
    from 0deg,
    #00e676, #00cfff, #ff4dff, #ffe135, #00e676
  );
  filter: blur(60px);
  animation: spin 8s linear infinite;
}

/* Cabeza del alien: sin imagen, solo HTML + CSS */
.alien-head {
  width: 80px; height: 100px;
  background: #00e676;
  border-radius: 50% 50% 45% 45%;
  border: 4px solid #000;
}
```

**Cero imágenes. Todo dibujado con CSS.**

---

## 🃏 Cards de destinos — Jordi

```html
<ul class="cards-grid">
  <li>
    <article class="card card--rainbow">
      <p class="card-emoji">🌈</p>
      <h3 class="card-title">Rainbow Lag Simulator</h3>
      <p class="card-desc">Colores imposibles, conversaciones profundas…</p>
      <button class="btn btn-card">Despegar 🚀</button>
    </article>
  </li>
  <!-- × 9 destinos -->
</ul>
```

`<article>` porque cada tarjeta es contenido **independiente y auto-contenido**.  
`<ul>` porque es una **colección de ítems** del mismo tipo.

---

## 🔲 Grid automático

```css
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 28px;
}
```

**Comportamiento responsivo sin media queries:**

```
Escritorio (>900px)    Tablet (600-900px)    Móvil (<600px)
┌────┐ ┌────┐ ┌────┐   ┌────┐ ┌────┐        ┌──────────┐
│    │ │    │ │    │   │    │ │    │        │          │
└────┘ └────┘ └────┘   └────┘ └────┘        └──────────┘
┌────┐ ┌────┐ ┌────┐   ┌────┐ ┌────┐        ┌──────────┐
│    │ │    │ │    │   │    │ │    │        │          │
└────┘ └────┘ └────┘   └────┘ └────┘        └──────────┘
   3 columnas               2                    1
```

`auto-fill` + `minmax` lo ajusta **solo**.

---

## 🎨 Color temático por card

Cada tarjeta tiene su modificador CSS con su propio color:

```css
.card--rainbow { --card-accent: #ff4dff; border-color: #9900cc; }
.card--forest  { --card-accent: #00e676; border-color: #006633; }
.card--astral  { --card-accent: #00cfff; border-color: #005577; }
.card--choco   { --card-accent: #ffb347; border-color: #7a3500; }
/* … y 6 más */

.card::before {
  background: var(--card-accent);
  opacity: 0.07;   /* capa de color muy sutil en el fondo */
}
```

Efecto hover: la card "salta" con sombra colorida.

```css
.card:hover { transform: translate(-4px, -4px); box-shadow: 10px 10px 0 #000; }
```

---

## 👽 Sobre nosotros — Edgar

```html
<section class="about-section">
  <div class="about-container">
    <h2>Nuestra misión</h2>
    <p>En <strong>Weed World</strong> creemos que los mejores viajes…</p>

    <!-- <dl>: lista de definiciones — ideal para etiqueta + valor -->
    <dl class="about-stats">
      <div class="stat">
        <dt class="stat-label">Dimensiones disponibles</dt>
        <dd class="stat-num">∞</dd>
      </div>
      <!-- … -->
    </dl>
  </div>

  <div class="about-ufo" aria-hidden="true">…</div>
</section>
```

`<dl>` es el elemento semántico correcto para **pares término–valor** (estadísticas).

---

## 🛸 OVNI animado — CSS puro

```css
/* Cúpula */
.ufo-dome {
  width: 70px; height: 40px;
  background: linear-gradient(180deg, rgba(0,207,255,0.8), rgba(0,207,255,0.3));
  border-radius: 50% 50% 0 0;
}

/* Luces parpadeantes con pseudo-elementos */
.ufo-base::before, .ufo-base::after {
  content: '';
  background: #00e676;
  border-radius: 50%;
  animation: blink 1.2s ease-in-out infinite alternate;
}
.ufo-base::after { animation-delay: 0.6s; }  /* desfase = efecto alterno */
```

```
      ╭───────╮    ← cúpula (.ufo-dome)
  ●───────────────●  ← platillo (.ufo-base) con luces
      ▽▽▽▽▽▽     ← rayo tractor (.ufo-beam)
```

---

## 🔘 Botones — sistema compartido

```css
/* Base: estilo flat comic con sombra desplazada */
.btn {
  font-family: var(--font-head);
  border: 3px solid #000;
  box-shadow: 4px 4px 0 #000;
  transition: transform 0.1s, box-shadow 0.1s;
}

/* Se "hunde" al pulsar */
.btn:active { transform: translate(2px, 2px); box-shadow: 2px 2px 0 #000; }

/* Hero: verde, más grande, con pulso de brillo */
.btn-hero { background: #00e676; animation: pulse-glow 2s ease-in-out infinite; }

/* Cards: amarillo Morty, ocupa el ancho completo */
.btn-card { background: #ffe135; width: 100%; margin-top: auto; }
```

`margin-top: auto` en flexbox empuja el botón **siempre al fondo** de la card.

---

## 📱 Diseño responsivo

```css
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;   /* apila logo + links + tagline */
    text-align: center;
  }

  .hero-alien  { display: none; }   /* no hay espacio en móvil */
  .about-ufo   { display: none; }   /* ídem con el OVNI */

  .cards-grid {
    grid-template-columns: 1fr;     /* una sola columna */
  }
}

@media (max-width: 480px) {
  .hero-title { font-size: 2.2rem; }   /* título más pequeño */
}
```

Estrategia **desktop-first**: el CSS base es para escritorio y los `@media` ajustan para móvil.

---

## ♿ Accesibilidad

| Técnica | Dónde | Por qué |
|---------|-------|---------|
| `aria-hidden="true"` | Estrellas, alien, OVNI, portal | Decorativos — lectores de pantalla los omiten |
| `aria-label` | `<nav>` | Identifica el bloque de navegación |
| `aria-labelledby` | `<section>` hero, destinos, about | Vincula la sección con su `<h2>` |
| `<address>` | Footer | Semántica correcta para datos de contacto |
| `<article>` | Cards | Contenido independiente y reutilizable |
| `<dl>` | Estadísticas | Par término–valor semántico |
| `role="list"` | Nav `<ul>` | Restablece semántica de lista en algunos navegadores |

---

## ✨ Animaciones — resumen

```css
@keyframes float    { 50% { transform: translateY(-12px); } }  /* levitación */
@keyframes spin     { to  { transform: rotate(360deg);    } }  /* portal */
@keyframes twinkle  { 100%{ opacity: 1; }                  }  /* estrellas */
@keyframes pulse-glow { 50% { box-shadow: …rgba(0,230,118,0.4); } } /* botón */
@keyframes blink    { to  { opacity: 1; }                  }  /* luces OVNI */
@keyframes beam-pulse{ 50% { opacity: 1; }                 }  /* rayo OVNI */
```

Todas usan **`ease-in-out`** o **`linear`** — sin JS, solo CSS.

---

## 👥 Reparto de trabajo

| Miembro | Secciones | Clases CSS principales |
|---------|-----------|------------------------|
| **Boris** | Navbar + Hero + Fuente | `.navbar` `.hero` `.portal-ring` `.hero-alien` |
| **Jordi** | Galería de cards | `.cards-section` `.cards-grid` `.card` `.btn-card` |
| **Edgar** | Sobre nosotros + Footer | `.about-section` `.about-ufo` `.footer` |
| **Roger** | Formularios + Animaciones | `@keyframes` · efectos hover · transiciones |

---

## 🏁 Tecnologías usadas

```
HTML5 semántico     → estructura y accesibilidad
CSS3 puro           → diseño, animaciones y responsividad
Google Fonts        → Bangers (títulos) + Nunito (cuerpo)
Git                 → control de versiones y trabajo en equipo
```

**Sin frameworks · Sin JavaScript · Sin librerías externas**

> El objetivo era demostrar dominio del lenguaje nativo antes  
> de introducir herramientas que lo abstraigan.

---

# 🛸 FIN

**Weed World** — Viajes a dimensiones que probablemente no deberías visitar.

> "No vendemos viajes. Vendemos historias que contar."

*Boris · Jordi · Edgar · Roger — 2026*
