<template>
  <div class="projects-section">

    <!-- LEFT SIDEBAR -->
    <aside class="sidebar">
      <div class="sidebar-label">// PROJECTS</div>
      <nav class="project-nav">
        <div
          v-for="(project, index) in projects"
          :key="project.id"
          class="nav-item"
          :class="{ active: activeIndex === index }"
          @click="selectProject(index)"
        >
          <span class="nav-arrow">&gt;&gt;</span>
          <span class="nav-title">{{ project.name }}</span>
        </div>
      </nav>

      <div class="sidebar-counter">
        <span class="counter-current">{{ String(activeIndex + 1).padStart(2, '0') }}</span>
        <span class="counter-sep"> / </span>
        <span class="counter-total">{{ String(projects.length).padStart(2, '0') }}</span>
      </div>
    </aside>

    <!-- RIGHT CONTENT -->
    <main class="project-content">
      <Transition name="slide" mode="out-in">
        <div class="project-detail" :key="activeIndex">

          <!-- Header -->
          <div class="detail-header">
            <h2 class="detail-title">{{ active.name }}</h2>
            <p class="detail-sub">{{ active.subtitle }}</p>
          </div>

          <!-- CTA-Visual ("Dein Projekt") -->
          <div v-if="isCta" class="cta-visual">
            <div class="cta-visual-inner">
              <span class="cta-plus">+</span>
              <span class="cta-visual-text">Dein Projekt</span>
            </div>
          </div>

          <!--PDF-->
          <div v-else-if="active.pdf" class="pdf-preview-card" @click="downloadPdf(active.pdf)">
    <img :src="active.pdfThumbnail" class="pdf-thumbnail-img" alt="PDF Vorschau" />
    
    <div class="pdf-overlay">
      <span class="pdf-icon">📄</span>
      <div class="pdf-info">
        <span class="pdf-label">// DOCUMENT_VIEW</span>
        <span class="pdf-name">{{ active.name }}.pdf</span>
      </div>
      <div class="pdf-download-hint">KLICKEN ZUM ÖFFNEN</div>
    </div>
  </div>

  <div v-else class="screenshots">
    <button class="carousel-btn prev" @click="prevShot">‹</button>
    <div class="carousel-track">
      <Transition name="carousel" mode="out-in">
        <div class="carousel-main" :key="activeShot">
          <video
            v-if="active.screenshots[activeShot] && isVideo(active.screenshots[activeShot]!)"
            :src="active.screenshots[activeShot]!"
            autoplay
            loop
            muted
            playsinline
            controls
          ></video>
          <img v-else-if="active.screenshots[activeShot]" :src="active.screenshots[activeShot]!" />
          <div v-else class="screenshot-placeholder featured">
            <span>{{ String(activeShot + 1).padStart(2, '0') }}</span>
          </div>
        </div>
      </Transition>
    </div>
    <div class="carousel-thumbs">
      <div v-for="(shot, i) in active.screenshots" :key="i" 
           class="thumb" :class="{ active: activeShot === i }" @click="activeShot = i">
        <video v-if="shot && isVideo(shot)" :src="shot" muted playsinline></video>
        <img v-else-if="shot" :src="shot" />
        <div v-else class="thumb-placeholder">{{ String(i + 1).padStart(2, '0') }}</div>
      </div>
    </div>
    <button class="carousel-btn next" @click="nextShot">›</button>
  </div>
          <div v-if="active.docs?.length" class="doc-widgets">
            <div
              v-for="doc in active.docs"
              :key="doc.label"
              class="doc-widget"
              @click="downloadPdf(doc.file)"
            >
              <span class="doc-icon">📄</span>
              <span class="doc-label">{{ doc.label }}</span>
              <span class="doc-dl">↓</span>
            </div>
          </div>
          <!-- Description -->
          <p class="detail-desc">{{ active.description }}</p>

          <!-- CTA-Karte statt Tech-Stack/Highlights-Grid -->
          <div v-if="isCta" class="cta-card-single">
            <div class="card-label">// WARUM MIT MIR ARBEITEN</div>
            <ul class="highlight-list">
              <li v-for="point in active.highlights" :key="point">
                <span class="bullet">▸</span>{{ point }}
              </li>
            </ul>
            <button class="cta-button" @click="$emit('open-contact', 'Neue Website')">
              Jetzt Projekt anfragen
            </button>
          </div>

          <!-- Bottom Cards -->
          <div v-else class="detail-cards">

            <!-- Tech Stack -->
            <div class="card tech-card">
              <div class="card-label">// {{ active.techLabel ?? 'TECH STACK' }}</div>

              <div v-if="active.techMode !== 'topics'" class="skill-list">
                <div
                  v-for="(skill, i) in active.skills"
                  :key="skill.name"
                  class="skill-row"
                  :style="{ animationDelay: `${i * 0.1}s` }"
                >
                  <span class="skill-name">{{ skill.name }}</span>
                  <div class="skill-bar-wrp">
                    <div
                      class="skill-bar-fill"
                      :style="{ width: skill.level + '%', transitionDelay: `${i * 0.1 + 0.3}s` }"
                    ></div>
                  </div>
                  <span class="skill-pct">{{ skill.level }}%</span>
                </div>
              </div>

              <ul v-else class="highlight-list">
                <li v-for="topic in active.topics" :key="topic">
                  <span class="bullet">▸</span>{{ topic }}
                </li>
              </ul>
            </div>

            <!-- Highlights -->
            <div class="card highlights-card">
              <div class="card-label">// HIGHLIGHTS</div>
              <ul class="highlight-list">
                <li v-for="point in active.highlights" :key="point">
                  <span class="bullet">▸</span>{{ point }}
                </li>
              </ul>

              <a v-if="active.link" :href="active.link" target="_blank" class="project-link">
                <span>PROJEKT ANSEHEN</span>
                <span class="link-arrow">→</span>
              </a>
            </div>

          </div>
        </div>
      </Transition>
    </main>

  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from 'vue';

import stockpileImg1 from '@/assets/img/Stockpile/Desktop-Mobile-View.jpeg'
import stockpileImg2 from '@/assets/img/Stockpile/Old_vs_new_v2.png'
import stockpileImg3 from '@/assets/img/Stockpile/Login_screen.jpeg'
import stockpilePlakat from '@/assets/doc/StockpilePlakat.pdf'
import stockpileBericht from '@/assets/doc/StockpileBericht.pdf'
import stockpileZeugnis from '@/assets/doc/StockpileZeugnis.pdf'

import shhWholevid from '@/assets/img/Shh.bar/ShhWholeWebNew.mp4'
import shhMobileResponsive from '@/assets/img/Shh.bar/MobileResponsive.jpg'

// TODO: Screenshots (oder kurze Videos!) von der shh.-Demo hier ablegen
// (z.B. /assets/img/Shh/) und die Imports unten aktivieren.
// Bilder: .jpeg/.png/.webp — normale Screenshots (ca. 1200x800px reicht).
// Videos: .mp4/.webm — z.B. ein 5-10 Sek. Screen-Recording der Ring-Pulse-
// Animation im Hero. Wird automatisch anhand der Dateiendung erkannt und
// im Carousel als <video> mit Autoplay/Loop/Controls dargestellt.
// import shhImg1 from '@/assets/img/Shh/hero.jpeg'
// import shhVideo1 from '@/assets/img/Shh/hero-animation.mp4'
// import shhImg2 from '@/assets/img/Shh/events.jpeg'
// import shhImg3 from '@/assets/img/Shh/drinks.jpeg'

const activeIndex = ref(0);

interface Project {
  id: string;
  name: string;
  subtitle: string;
  description: string;
  screenshots: (string | null)[];
  pdf?: string;
  pdfThumbnail?: string;
  docs?: { label: string; file: string }[];
  techLabel?: string;        // ← neu
  techMode?: 'skills' | 'topics'; // ← neu
  topics?: string[];         // ← neu
  skills: { name: string; level: number }[];
  highlights: string[];
  link: string;
}

const projects = [
  {
    id: 'shh-listening-bar',
    name: 'Shh. Listening Bar',
    subtitle: 'Konzept-Website für eine Wiener Listening Bar (Eigeninitiative)',
    description: 'Unaufgefordert entwickeltes Website-Konzept für eine Wiener Listening Bar — von der Recherche über das Design bis zur live geschalteten Demo. Kernstück ist eine Event-Übersicht, die der Betrieb komplett selbst über ein einfaches Google Sheet pflegen könnte, ganz ohne Programmierkenntnisse oder Login-Bereich.',
    // Sobald Screenshots vorhanden sind: [shhImg1, shhImg2, shhImg3]
    screenshots: [shhWholevid, shhMobileResponsive],
    techLabel: 'TECH STACK',
    techMode: 'skills',
    skills: [
      { name: 'HTML/CSS/JS', level: 90 },
      { name: 'Design System', level: 85 },
      { name: 'Google Sheets API', level: 75 },
      { name: 'Hosting/Deploy', level: 80 },
    ],
    highlights: [
      'Individuelles Design, abgestimmt auf bestehende Marke & Bildsprache (Farben, Typografie, Fotomaterial)',
      'Self-Service Event-Pflege via Google Sheet — Betrieb könnte Events selbst eintragen, keine Code-Kenntnisse nötig',
      'Von Konzept-Idee bis live geschalteter Demo in unter einer Woche umgesetzt',
    ],
    link: '#', // hier den echten Netlify-Link einfügen, sobald live
  },
  {
    id: 'stockpile',
    name: 'STOCKPILE',
    subtitle: 'Intelligentes Lagerverwaltungssystem',
    description: 'Entwicklung eines responsiven Frontend-Interfaces für ein internes Lagerverwaltungssystem mit Anbindung an eine bestehende GraphQL-Schnittstelle, optimiert für Desktop und Zebra-Scanner',
    screenshots: [stockpileImg1, stockpileImg2, stockpileImg3],
    skills: [
      { name: 'Vue.js', level: 75 },
      { name: 'TypeScript', level: 65 },
      { name: 'HTML5', level: 80 },
      { name: 'CSS/SCSS', level: 80 },
      { name: 'Node.js', level: 55 },
    ],
    docs: [
      { label: 'PLAKAT', file: stockpilePlakat },
      { label: 'ZEUGNIS', file: stockpileZeugnis },
      { label: 'FACHBERICHT', file: stockpileBericht },
    ],
    highlights: [
      'Kernfunktionen wie Einlagern, Entnahme und Umlagern wurden erfolgreich umgesetzt',
      'Die Oberfläche wurde für mobile Zebra-Scanner und den Desktop getrennt optimiert',
      'LDAP-Sicherung und Anbindung an das Windows AD wurden berücksichtigt',
    ],
    link: '#',
  },
  {
    id: 'cta',
    name: 'Dein Projekt',
    subtitle: 'Hier könnte schon bald dein Projekt entstehen',
    description: 'Egal ob Restaurant, Bar, kleiner Shop oder Dienstleistung — wenn du eine Website brauchst, die zu deinem Business passt statt nach Template auszusehen, lass uns reden.',
    screenshots: [],
    skills: [],
    highlights: [
      'Individuelles Design statt austauschbarem Template',
      'Self-Service-Backend, wenn du Inhalte selbst pflegen willst',
      'Von der ersten Idee bis live geschaltet in wenigen Tagen',
    ],
    link: '#',
  },
];

const emit = defineEmits<{
  (e: 'open-contact', reason: string): void;
}>();

const active = computed<Project>(() => (projects[activeIndex.value] ?? projects[0]) as Project);
const isCta = computed(() => active.value.id === 'cta');

// Erkennt anhand der Dateiendung, ob ein Eintrag ein Video statt eines Bildes ist
function isVideo(src: string): boolean {
  return /\.(mp4|webm|mov|ogg)$/i.test(src);
}

    const activeShot = ref(0);

// activeShot zurücksetzen wenn Projekt wechselt
watch(activeIndex, () => {
  activeShot.value = 0;
});

function prevShot() {
  activeShot.value = (activeShot.value - 1 + active.value.screenshots.length) % active.value.screenshots.length;
}

function nextShot() {
  activeShot.value = (activeShot.value + 1) % active.value.screenshots.length;
}

function selectProject(index: number) {
  activeIndex.value = index;
}

function downloadPdf(url: string) {
  const link = document.createElement('a');
  link.href = url;
  link.setAttribute('download', ''); // Triggert den Download-Dialog
  link.setAttribute('target', '_blank');
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
}
</script>

<style lang="scss" scoped>
@use "../assets/variables.scss" as *;

$neon: #b4f000;
$blue: #00aaff;
$dark: #111111;
$sidebar-bg: #0a0a0a;
$dim: #333;
$text-muted: #666;

/* ── LAYOUT ── */
.projects-section {
  display: flex;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  background-color: $dark;
  font-family: 'Dogica Pixel', monospace;
}

/* ── SIDEBAR ── */
.sidebar {
  width: 320px;
  flex-shrink: 0;
  background-color: $sidebar-bg;
  display: flex;
  flex-direction: column;
  padding: 60px 0 40px 40px;
  border-right: 1px solid #1a1a1a;
  position: relative;
}

.sidebar-label {
  font-size: 9px;
  color: $neon;
  letter-spacing: 4px;
  margin-bottom: 40px;
  opacity: 0.7;
}

.project-nav {
  display: flex;
  flex-direction: column;
  gap: 28px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
  opacity: 0.35;
  transition: opacity 0.3s;

  &:hover {
    opacity: 0.7;
  }

  &.active {
    opacity: 1;

    .nav-arrow {
      color: $blue;
    }

    .nav-title {
      color: $blue;
      text-shadow: 0 0 20px rgba($blue, 0.5);

      // Glitch effect on active
      animation: glitch 4s infinite;
    }
  }
}

.nav-arrow {
  font-size: 12px;
  color: $dim;
  transition: color 0.3s;
  flex-shrink: 0;
}

.nav-title {
  font-size: 14px;
  color: #aaa;
  letter-spacing: 2px;
  transition: color 0.3s;
}

@keyframes glitch {
  0%, 90%, 100% { text-shadow: 0 0 20px rgba($blue, 0.5); transform: none; }
  91% { transform: translateX(-2px); text-shadow: 2px 0 $neon, -2px 0 $blue; }
  92% { transform: translateX(2px); text-shadow: -2px 0 $neon, 2px 0 $blue; }
  93% { transform: none; text-shadow: 0 0 20px rgba($blue, 0.5); }
}

.sidebar-counter {
  margin-top: auto;
  margin-bottom: 40px;
  font-size: 11px;
  color: $dim;
  letter-spacing: 2px;

  .counter-current {
    color: $neon;
    font-size: 22px;
  }
}

/* ── CONTENT ── */
.project-content {
  flex: 1;
  padding: 60px 70px;
  overflow-y: auto;
  background-color: #f5f5f5;
}

.project-detail {
  max-width: 860px;
}

/* ── HEADER ── */
.detail-header {
  margin-bottom: 32px;

  .detail-title {
    font-size: clamp(24px, 3vw, 40px);
    color: #111;
    margin: 0 0 8px;
    letter-spacing: 3px;
  }

  .detail-sub {
    font-size: 11px;
    color: $blue;
    margin: 0;
    letter-spacing: 2px;
  }
}

/* ── SCREENSHOTS ── */
/* ── CAROUSEL ── */
.screenshots {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 36px;
}

.carousel-btn {
  background: none;
  border: 1px solid #ccc;
  color: #666;
  font-size: 24px;
  width: 36px;
  height: 36px;
  border-radius: 4px;
  cursor: pointer;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color 0.2s, color 0.2s;
  line-height: 1;

  &:hover {
    border-color: $blue;
    color: $blue;
  }
}

.carousel-track {
  flex: 1;
  aspect-ratio: 16/9;
  border-radius: 6px;
  overflow: hidden;
  background: #1a1a1a;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  video {
    width: 100%;
    height: 100%;
    object-fit: contain; // Video wird komplett eingepasst statt beschnitten
  }
}

.screenshot-placeholder.featured {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #1a1a1a, #0a0a0a);

  span {
    font-family: 'Dogica Pixel', monospace;
    font-size: 32px;
    color: #2a2a2a;
  }
}

/* ── CTA VISUAL ("Dein Projekt") ── */
.cta-visual {
  width: 100%;
  aspect-ratio: 16/9;
  border-radius: 6px;
  margin-bottom: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #1a1a1a, #0a0a0a);
  border: 2px dashed rgba($blue, 0.25);
  transition: border-color 0.3s;

  &:hover {
    border-color: rgba($blue, 0.5);
  }

  .cta-visual-inner {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }

  .cta-plus {
    font-family: 'Dogica Pixel', monospace;
    font-size: 40px;
    color: rgba($blue, 0.35);
    line-height: 1;
  }

  .cta-visual-text {
    font-family: 'Dogica Pixel', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    color: #444;
    text-transform: uppercase;
  }
}

.carousel-thumbs {
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex-shrink: 0;
}

.thumb {
  width: 80px;
  aspect-ratio: 16/9;
  border-radius: 3px;
  overflow: hidden;
  cursor: pointer;
  opacity: 0.4;
  border: 2px solid transparent;
  transition: opacity 0.2s, border-color 0.2s;

  &.active {
    opacity: 1;
    border-color: $blue;
  }

  &:hover {
    opacity: 0.7;
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  video {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
}

.thumb-placeholder {
  width: 100%;
  height: 100%;
  background: #1a1a1a;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: #333;
}

/* ── CAROUSEL TRANSITION ── */
.carousel-enter-active,
.carousel-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.carousel-enter-from {
  opacity: 0;
  transform: translateX(15px);
}

.carousel-leave-to {
  opacity: 0;
  transform: translateX(-15px);
}

/* ── DESCRIPTION ── */
.detail-desc {
  font-family: sans-serif;
  font-size: 14px;
  color: #444;
  line-height: 1.9;
  margin: 0 0 36px;
}

/* ── CARDS ── */
.detail-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.card {
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
  padding: 24px 28px;

  .card-label {
    font-family: 'Dogica Pixel', monospace;
    font-size: 8px;
    color: $blue;
    letter-spacing: 3px;
    margin-bottom: 20px;
    opacity: 0.8;
  }
}

/* ── SKILL BARS ── */
.skill-list {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.skill-row {
  display: flex;
  align-items: center;
  gap: 12px;
}

.skill-name {
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  line-height: 1.6;
  color: #555;
  width: 70px;
  flex-shrink: 0;
}

.skill-bar-wrp {
  flex: 1;
  height: 4px;
  background: #e0e0e0;
  border-radius: 2px;
  overflow: hidden;
}

.skill-bar-fill {
  height: 100%;
  background: $blue;
  border-radius: 2px;
  width: 0;
  transition: width 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.skill-pct {
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: $blue;
  width: 36px;
  text-align: right;
  flex-shrink: 0;
}

/* ── HIGHLIGHTS ── */
.highlight-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;

  li {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    font-family: sans-serif;
    font-size: 13px;
    color: #444;
  }

  .bullet {
    color: $blue;
    font-size: 10px;
    margin-top: 2px;
    flex-shrink: 0;
  }
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin-top: 24px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: $blue;
  text-decoration: none;
  letter-spacing: 2px;
  border-bottom: 1px solid rgba($blue, 0.3);
  padding-bottom: 4px;
  transition: gap 0.2s, border-color 0.2s;

  &:hover {
    gap: 18px;
    border-color: $blue;
  }

  .link-arrow {
    font-size: 14px;
  }
}

/* ── CTA CARD ("Dein Projekt") ── */
.cta-card-single {
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
  padding: 30px 32px;

  .card-label {
    font-family: 'Dogica Pixel', monospace;
    font-size: 8px;
    color: $blue;
    letter-spacing: 3px;
    margin-bottom: 20px;
    opacity: 0.8;
  }

  .highlight-list {
    margin-bottom: 26px;
  }
}

.cta-button {
  width: 100%;
  font-family: 'Dogica Pixel', monospace;
  font-size: 11px;
  letter-spacing: 1px;
  color: #111;
  background: $neon;
  border: none;
  padding: 16px 0;
  border-radius: 6px;
  cursor: pointer;
  transition: filter 0.2s, transform 0.2s;

  &:hover {
    filter: brightness(1.08);
    transform: translateY(-1px);
  }
}

/* ── SLIDE TRANSITION ── */
.slide-enter-active,
.slide-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(20px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-20px);
}

.pdf-preview-card {
  position: relative;
  width: 100%;
  aspect-ratio: 16/9;
  border-radius: 6px;
  overflow: hidden;
  background: #000;
  cursor: pointer;
  margin-bottom: 36px;
  border: 1px solid #333;

  .pdf-thumbnail-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0.5; // Leicht abdunkeln für das Overlay
    transition: transform 0.5s ease, opacity 0.3s;
  }

  .pdf-overlay {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: rgba($dark, 0.4); // Glas-Effekt
    backdrop-filter: blur(2px);
    border: 2px dashed rgba($blue, 0.3);
    margin: 10px;
    border-radius: 4px;
    transition: all 0.3s ease;
  }

  &:hover {
    .pdf-thumbnail-img { transform: scale(1.05); opacity: 0.7; }
    .pdf-overlay { 
      background: rgba($blue, 0.1); 
      border-color: $blue;
    }
    .pdf-icon { transform: scale(1.2); color: $neon; }
  }

  .pdf-icon {
    font-size: 50px;
    margin-bottom: 15px;
    transition: all 0.3s;
  }

  .pdf-info {
    text-align: center;
    margin-bottom: 15px;
    .pdf-label { display: block; font-size: 8px; color: $blue; letter-spacing: 2px; }
    .pdf-name { font-size: 14px; color: #fff; font-family: 'Dogica Pixel', monospace; }
  }

  .pdf-download-hint {
    font-size: 9px;
    padding: 6px 12px;
    border: 1px solid $blue;
    color: $blue;
  }
}

.doc-widgets {
  display: flex;
  gap: 10px;
  margin-bottom: 28px;
  flex-wrap: wrap;
}

.doc-widget {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  padding: 14px 18px;
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
  cursor: pointer;
  transition: border-color 0.2s, transform 0.2s;
  min-width: 90px;

  &:hover {
    border-color: $blue;
    transform: translateY(-2px);
  }

  .doc-icon { font-size: 22px; }

  .doc-label {
    font-family: 'Dogica Pixel', monospace;
    font-size: 7px;
    color: #555;
    letter-spacing: 1px;
    text-align: center;
  }

  .doc-dl {
    font-size: 12px;
    color: $blue;
  }
}

/* ══════════════ MOBILE ══════════════ */
@media (max-width: 900px) {
  .projects-section {
    flex-direction: column;
    height: auto;
    min-height: auto;
    overflow: visible;
  }

  .sidebar {
    width: 100%;
    flex-direction: row;
    align-items: center;
    overflow-x: auto;
    padding: 24px 20px;
    border-right: none;
    border-bottom: 1px solid #1a1a1a;
  }

  .sidebar-label {
    display: none;
  }

  .project-nav {
    flex-direction: row;
    gap: 24px;
  }

  .nav-item {
    white-space: nowrap;
  }

  .sidebar-counter {
    display: none;
  }

  .project-content {
    padding: 32px 24px 60px;
  }

  .detail-cards {
    grid-template-columns: 1fr;
  }

  .screenshots {
    gap: 10px;
  }

  .carousel-thumbs {
    flex-direction: row;
    overflow-x: auto;
  }

  .thumb {
    width: 64px;
    flex-shrink: 0;
  }
}
</style>