<template>
  <div class="hero" ref="heroRef">

    <!-- Background SVG diagonal split -->
    <div class="hero-bg">
      <img class="hero-bg-svg" src="../assets/img/back-1.svg" />
    </div>

    <!-- Animated noise grain overlay -->
    <div class="hero-grain"></div>

    <!-- Floating particles -->
    <div class="particles">
      <span v-for="n in 12" :key="n" class="particle" :style="particleStyle(n)"></span>
    </div>

    <!-- NAV -->
    <nav class="hero-nav">
      <div class="nav-logo">&lt;PD /&gt;</div>
      <div class="nav-links">
        <a href="#projects" @click.prevent="scrollTo('projects')">Projects</a>
        <a href="#packages" @click.prevent="scrollTo('packages')">Leistungen</a>
        <a href="#lebenslauf" @click.prevent="scrollTo('lebenslauf')">Werdegang</a>
        <a href="#about" @click.prevent="scrollTo('about')">Über mich</a>
      </div>
      <button class="nav-contact" @click="$emit('open-contact', 'Sonstiges')">
        <svg width="18" height="18" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
          <path d="M440.917,67.925H71.083C31.827,67.925,0,99.752,0,139.008v233.984c0,39.256,31.827,71.083,71.083,71.083h369.834c39.255,0,71.083-31.827,71.083-71.083V139.008C512,99.752,480.172,67.925,440.917,67.925z M256,289.436c-13.314-0.033-26.22-4.457-36.31-13.183L66.962,143.694c-6.98-6.058-7.723-16.612-1.674-23.583c6.057-6.98,16.612-7.723,23.582-1.674l152.771,132.592c3.265,2.906,8.645,5.004,14.359,4.971c5.706,0.017,10.995-2.024,14.44-5.028l152.615-132.469c6.971-6.049,17.526-5.306,23.583,1.674c6.048,6.97,5.306,17.525-1.674,23.583L292.31,276.253C282.211,284.929,269.322,289.419,256,289.436z"/>
        </svg>
        Kontakt
      </button>
    </nav>

    <!-- MAIN CONTENT -->
    <div class="hero-content">

      <!-- LEFT -->
      <div class="hero-left">

        <div class="hero-eyebrow">
          <span class="eyebrow-dot"></span>
          <span>Aktuell für neue Projekte verfügbar</span>
        </div>

        <h1 class="hero-title">
          <span class="title-line title-line--1">WEBENTWICKLUNG AUS WIEN</span>
          <span class="title-line title-line--2">PAUL<br>DOBRICK</span>
        </h1>

        <p class="hero-desc">
          Ich bin Paul, Web-Entwickler aus Wien — spezialisiert auf individuell
          gestaltete Websites mit modernem Frontend (KI-gestützt, schnell umgesetzt)
          und einem Backend, das mit deinem Business mitwächst. Keine austauschbaren
          Templates, sondern eine Seite, die zu dir passt.
        </p>

        <div class="hero-tags">
          <span class="tag">Individuelles Design</span>
          <span class="tag">Vue.js / TypeScript</span>
          <span class="tag">Backend & Datenbanken</span>
          <span class="tag">Self-Service Content</span>
          <span class="tag">Wien</span>
        </div>

        <div class="hero-actions">
          <button class="btn-primary" @click="scrollTo('projects')">
            Projekte ansehen
            <span class="btn-arrow">→</span>
          </button>
          <button class="btn-secondary" @click="scrollTo('about')">
            Über mich
          </button>
        </div>

        <!-- Location -->
        <div class="hero-location">
          <svg width="14" height="14" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
            <path d="M253.924,127.592a64,64,0,1,0,64,64A64.073,64.073,0,0,0,253.924,127.592Zm0,96a32,32,0,1,1,32-32A32.037,32.037,0,0,1,253.924,223.592Z"/>
            <path d="M376.906,68.515A173.922,173.922,0,0,0,108.2,286.426L229.107,472.039a29.619,29.619,0,0,0,49.635,0L399.653,286.426A173.921,173.921,0,0,0,376.906,68.515Zm-4.065,200.444L253.925,451.509,135.008,268.959C98.608,213.08,106.415,138.3,153.571,91.142a141.92,141.92,0,0,1,200.708,0C401.435,138.3,409.241,213.08,372.841,268.959Z"/>
          </svg>
          <span>Wien, Österreich</span>
          <span class="location-sep">·</span>
          <span>Einzelunternehmen</span>
        </div>

      </div>

      <!-- RIGHT: Photo -->
      <div class="hero-right">
        <div class="photo-frame">
          <div class="photo-ring photo-ring--outer"></div>
          <div class="photo-ring photo-ring--inner"></div>
          <div class="photo-circle">
            <img src="../assets/img/Main-Portfolio-Pauk.jpeg" alt="Paul Dobrick" />
          </div>
          <!-- Floating badge -->
          <div class="photo-badge">
            <span class="badge-dot"></span>
            <span>Open for Projects</span>
          </div>
          <!-- Corner decoration -->
          <div class="photo-corner tl"></div>
          <div class="photo-corner tr"></div>
        </div>
      </div>

    </div>

    <!-- BOTTOM BAR -->
    <div class="hero-bottom">
      <div class="social-links">
        <!-- GitHub -->
        <a href="https://github.com/pauldobrick-dev" id="github" class="social-link" title="GitHub" target="_blank" rel="noopener">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
          </svg>
        </a>
        <!-- LinkedIn -->
        <a href="https://www.linkedin.com/in/paul-dobrick-43607337b/" id="linkedin" class="social-link" title="LinkedIn" target="_blank" rel="noopener">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
          </svg>
        </a>
      </div>

      <div class="scroll-hint" :class="{ hidden: scrolled }">
        <span>SCROLL</span>
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
          <path d="M7 13L12 18L17 13M7 6L12 11L17 6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>

      <div class="hero-counter">
        <span>01</span><span class="counter-div">/</span><span>05</span>
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const emit = defineEmits<{
  (e: 'open-contact', reason: string): void;
}>();

const scrolled = ref(false);
const heroRef = ref<HTMLElement | null>(null);

function onScroll() {
  scrolled.value = window.scrollY > 50;
}

onMounted(() => window.addEventListener('scroll', onScroll));
onUnmounted(() => window.removeEventListener('scroll', onScroll));

function scrollTo(id: string) {
  const el = document.getElementById(id);
  el?.scrollIntoView({ behavior: 'smooth' });
}

function particleStyle(n: number) {
  const size = 2 + (n % 3);
  return {
    left: `${(n * 137.5) % 100}%`,
    top: `${(n * 97.3) % 100}%`,
    width: `${size}px`,
    height: `${size}px`,
    animationDelay: `${(n * 0.7) % 4}s`,
    animationDuration: `${4 + (n % 4)}s`,
  };
}
</script>

<style lang="scss" scoped>
@use "../assets/variables.scss" as *;

$neon: #b4f000;
$dark: #111111;
$white: #f5f5f5;

/* ── HERO ── */
.hero {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

/* ── BACKGROUND ── */
.hero-bg {
  position: absolute;
  inset: 0;
  z-index: 0;

  .hero-bg-svg {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}

.hero-grain {
  position: absolute;
  inset: 0;
  z-index: 1;
  opacity: 0.035;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  background-size: 150px;
  pointer-events: none;
}

/* ── PARTICLES ── */
.particles {
  position: absolute;
  inset: 0;
  z-index: 1;
  pointer-events: none;
}

.particle {
  position: absolute;
  border-radius: 50%;
  background: $neon;
  opacity: 0;
  animation: particle-float linear infinite;
}

@keyframes particle-float {
  0%   { opacity: 0; transform: translateY(0) scale(1); }
  10%  { opacity: 0.4; }
  90%  { opacity: 0.1; }
  100% { opacity: 0; transform: translateY(-80px) scale(0.5); }
}

/* ── NAV ── */
.hero-nav {
  position: relative;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24px 52px;
  flex-shrink: 0;
}

.nav-logo {
  font-family: 'Dogica Pixel', monospace;
  font-size: 14px;
  color: $neon;
  letter-spacing: 2px;
}

.nav-links {
  display: flex;
  gap: 36px;

  a {
    font-family: 'Dogica Pixel', monospace;
    font-size: 9px;
    color: #888;
    text-decoration: none;
    letter-spacing: 2px;
    transition: color 0.2s;

    &:hover { color: white; }
  }
}

.nav-contact {
  display: flex;
  align-items: center;
  gap: 8px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: #111;
  background: $neon;
  border: none;
  padding: 10px 18px;
  border-radius: 4px;
  cursor: pointer;
  letter-spacing: 1px;
  transition: filter 0.2s, transform 0.2s;

  &:hover {
    filter: brightness(1.1);
    transform: translateY(-1px);
  }
}

/* ── MAIN CONTENT ── */
.hero-content {
  flex: 1;
  position: relative;
  z-index: 5;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 52px;
  gap: 40px;
}

/* ── LEFT ── */
.hero-left {
  max-width: 560px;
  display: flex;
  flex-direction: column;
  gap: 24px;

  // Staggered entrance animations
  & > * {
    animation: fadeUp 0.7s ease both;
  }
  & > *:nth-child(1) { animation-delay: 0.1s; }
  & > *:nth-child(2) { animation-delay: 0.2s; }
  & > *:nth-child(3) { animation-delay: 0.35s; }
  & > *:nth-child(4) { animation-delay: 0.45s; }
  & > *:nth-child(5) { animation-delay: 0.55s; }
  & > *:nth-child(6) { animation-delay: 0.65s; }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero-eyebrow {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: #666;
  letter-spacing: 2px;
}

.eyebrow-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: $neon;
  box-shadow: 0 0 8px $neon;
  animation: pulse-dot 2s infinite;
  flex-shrink: 0;
}

@keyframes pulse-dot {
  0%, 100% { box-shadow: 0 0 4px $neon; }
  50% { box-shadow: 0 0 14px $neon; }
}

.hero-title {
  margin: 0;
  display: flex;
  flex-direction: column;
  line-height: 1;
}

.title-line {
  display: block;
  font-family: 'Dogica Pixel', monospace;

  &--1 {
    font-size: clamp(14px, 1.6vw, 20px);
    color: #555;
    letter-spacing: 6px;
    margin-bottom: 10px;
    font-weight: 400;
  }

  &--2 {
    font-size: clamp(38px, 10vw, 88px);
    color: $neon;
    letter-spacing: 2px;
    font-weight: 700;
    line-height: 0.95;
    // Subtle text shadow for depth
    text-shadow:
      0 0 40px rgba($neon, 0.3),
      0 2px 0 rgba(0,0,0,0.5);
  }
}

.hero-desc {
  font-family: sans-serif;
  font-size: 15px;
  color: #555;
  line-height: 1.8;
  margin: 0;
  max-width: 440px;
}

.hero-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tag {
  font-family: 'Dogica Pixel', monospace;
  font-size: 8px;
  color: #777;
  border: 1px solid #2a2a2a;
  padding: 5px 10px;
  border-radius: 3px;
  letter-spacing: 1px;
  transition: border-color 0.2s, color 0.2s;

  &:hover {
    border-color: rgba($neon, 0.5);
    color: $neon;
  }
}

.hero-actions {
  display: flex;
  gap: 16px;
  align-items: center;
}

.btn-primary {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 10px;
  color: #111;
  background: $neon;
  border: none;
  padding: 16px 28px;
  border-radius: 4px;
  cursor: pointer;
  letter-spacing: 1px;
  transition: filter 0.2s, transform 0.2s, gap 0.2s;

  &:hover {
    filter: brightness(1.08);
    transform: translateY(-2px);
    gap: 18px;
  }

  .btn-arrow {
    font-size: 16px;
    transition: transform 0.2s;
  }
}

.btn-secondary {
  font-family: 'Dogica Pixel', monospace;
  font-size: 10px;
  color: #888;
  background: transparent;
  border: 1px solid #2a2a2a;
  padding: 16px 24px;
  border-radius: 4px;
  cursor: pointer;
  letter-spacing: 1px;
  transition: border-color 0.2s, color 0.2s, transform 0.2s;

  &:hover {
    border-color: #555;
    color: white;
    transform: translateY(-2px);
  }
}

.hero-location {
  display: flex;
  align-items: center;
  gap: 8px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: #555;
  letter-spacing: 1px;

  svg { opacity: 0.5; flex-shrink: 0; }
  .location-sep { opacity: 0.3; }
}

/* ── RIGHT / PHOTO ── */
.hero-right {
  flex-shrink: 0;
  animation: fadeUp 0.8s ease 0.3s both;
}

.photo-frame {
  position: relative;
  width: 380px;
  height: 380px;
}

.photo-ring {
  position: absolute;
  border-radius: 50%;
  border: 1px solid rgba($neon, 0.15);
  animation: spin-slow linear infinite;

  &--outer {
    inset: -30px;
    animation-duration: 20s;
    border-style: dashed;
    border-color: rgba($neon, 0.1);
  }

  &--inner {
    inset: -12px;
    animation-duration: 12s;
    animation-direction: reverse;
    border-color: rgba($neon, 0.2);
    background: conic-gradient(from 0deg, rgba($neon, 0.08), transparent 40%, transparent 80%, rgba($neon, 0.08));
  }
}

@keyframes spin-slow {
  to { transform: rotate(360deg); }
}

.photo-circle {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid rgba($neon, 0.35);
  box-shadow:
    0 0 0 1px rgba($neon, 0.1),
    0 30px 80px rgba(0,0,0,0.5),
    inset 0 0 40px rgba(0,0,0,0.3);

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: top center;
    scale: 1.05; // slight zoom to fill better
  }
}

.photo-badge {
  position: absolute;
  bottom: 10px;
  left: -20px;
  background: rgba(17, 17, 17, 0.9);
  backdrop-filter: blur(12px);
  border: 1px solid rgba($neon, 0.25);
  border-radius: 30px;
  padding: 8px 16px;
  display: flex;
  align-items: center;
  gap: 8px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 8px;
  color: $neon;
  letter-spacing: 1px;
  white-space: nowrap;
  animation: badge-float 3s ease-in-out infinite;
}

.badge-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: $neon;
  box-shadow: 0 0 6px $neon;
  animation: pulse-dot 2s infinite;
}

@keyframes badge-float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-6px); }
}

.photo-corner {
  position: absolute;
  width: 20px;
  height: 20px;

  &.tl {
    top: -4px;
    left: -4px;
    border-top: 2px solid $neon;
    border-left: 2px solid $neon;
  }
  &.tr {
    top: -4px;
    right: -4px;
    border-top: 2px solid $neon;
    border-right: 2px solid $neon;
  }
}

/* ── BOTTOM BAR ── */
.hero-bottom {
  position: relative;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 52px 24px;
  flex-shrink: 0;
}

.social-links {
  display: flex;
  align-items: center;
  gap: 24px;
}

.social-link {
  color: inherit;
  text-decoration: none;
  display: flex;
  align-items: center;
}

#github {
  cursor: pointer;
  color: #b26bff;
  filter: drop-shadow(0 0 4px rgba(178, 107, 255, 0.5));
  transition: .2s ease-in-out all;

  &:hover {
    color: $neon;
    transform: translateY(-3px);
  }
}

#linkedin {
  cursor: pointer;
  color: #b26bff;
  filter: drop-shadow(0 0 4px rgba(178, 107, 255, 0.5));
  transition: .2s ease-in-out all;

  &:hover {
    color: $neon;
    transform: translateY(-3px);
  }
}

.scroll-hint {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 8px;
  color: #444;
  letter-spacing: 3px;
  transition: opacity 0.4s;
  animation: scroll-bounce 2.5s ease-in-out infinite;

  &.hidden { opacity: 0; }

  svg { color: #444; }
}

@keyframes scroll-bounce {
  0%, 100% { transform: translateY(0); opacity: 0.5; }
  50% { transform: translateY(6px); opacity: 1; }
}

.hero-counter {
  font-family: 'Dogica Pixel', monospace;
  font-size: 10px;
  color: #333;
  letter-spacing: 2px;

  .counter-div { margin: 0 4px; opacity: 0.4; }
}

/* ══════════════ MOBILE ══════════════ */
@media (max-width: 768px) {
  .hero {
    height: auto;
    min-height: 100vh;
  }

  .hero-nav {
    padding: 18px 20px;
  }

  .nav-links {
    display: none;
  }

  .nav-contact {
    display: none;
  }

  .hero-content {
    flex-direction: column-reverse;
    padding: 32px 24px 24px;
    gap: 32px;
    text-align: center;
  }

  .hero-left {
    max-width: 100%;
    align-items: center;
  }

  .hero-eyebrow,
  .hero-tags,
  .hero-actions,
  .hero-location {
    justify-content: center;
  }

  .hero-desc {
    max-width: 100%;
  }

  .hero-actions {
    flex-wrap: wrap;
  }

  .photo-frame {
    width: 220px;
    height: 220px;
  }

  .photo-badge {
    left: 50%;
    transform: translateX(-50%);
  }

  .hero-bottom {
    padding: 16px 20px 24px;
    flex-wrap: wrap;
    justify-content: center;
    gap: 14px;
  }

  .scroll-hint {
    display: none;
  }
}
</style>