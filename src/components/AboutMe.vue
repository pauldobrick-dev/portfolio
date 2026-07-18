<template>
  <div class="about-section" @mousemove="onMouseMove" @mouseleave="onMouseLeave">

    <!-- Background -->
    <div class="bg-grid"></div>
    <div class="bg-glow"></div>

    <div class="section-label">// ÜBER MICH</div>

    <!-- 3D CARD -->
    <div class="card-scene">
      <div
        class="card-3d"
        :style="{
          transform: `perspective(1000px) rotateY(${rotateY}deg) rotateX(${rotateX}deg)`,
        }"
      >
        <!-- CARD FRONT -->
        <div class="card-face front">

          <!-- Glare effect -->
          <div class="card-glare" :style="{ background: glareStyle }"></div>

          <!-- Top row -->
          <div class="card-top">
            <div class="card-tag">PAUL DOBRICK</div>
            <div class="card-id">ID // 2006</div>
          </div>

          <!-- Photo -->
          <div class="card-photo-wrp">
            <img class="card-photo" src="../assets/img/Paris.jpeg" alt="Paul Dobrick" />
            <div class="card-photo-border"></div>
          </div>

          <!-- Info -->
          <div class="card-info">
            <div class="info-row">
              <span class="info-label">NAME</span>
              <span class="info-value">Paul Dobrick</span>
            </div>
            <div class="info-row">
              <span class="info-label">ALTER</span>
              <span class="info-value">{{ age }} Jahre</span>
            </div>
            <div class="info-row">
              <span class="info-label">WOHNORT</span>
              <span class="info-value">Wien, AT</span>
            </div>
            <div class="info-row">
              <span class="info-label">STATUS</span>
              <span class="info-value status">
                <span class="status-dot"></span>Offen für Angebote
              </span>
            </div>
          </div>

          <!-- Hobbies -->
          <div class="card-hobbies">
            <span v-for="hobby in hobbies" :key="hobby" class="hobby-tag">{{ hobby }}</span>
          </div>

          <!-- Bottom bar -->
          <div class="card-bottom">
            <div class="card-stripe" v-for="n in 3" :key="n"></div>
          </div>

        </div>
      </div>
    </div>

    <!-- Side text -->
    <div class="side-text">
      <div class="side-block" v-for="(block, i) in sideBlocks" :key="i" :style="{ animationDelay: `${i * 0.15}s` }">
        <div class="side-block-label">{{ block.label }}</div>
        <div class="side-block-value">{{ block.value }}</div>
      </div>

      <p class="about-desc">
        {{ description }}
      </p>

      <div class="skill-chips">
        <span v-for="skill in skills" :key="skill" class="skill-chip">{{ skill }}</span>
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

// Alter automatisch berechnen
const birthYear = 2006;
const age = computed(() => new Date().getFullYear() - birthYear);

const hobbies = ['Web-Entwicklung', 'UI/UX Design', 'Backend & APIs', 'KI-gestütztes Coding'];

const description = `Ich baue individuelle Websites für Unternehmen in Wien — von der ersten Idee bis zur Live-Schaltung. Mein Fokus: schnelle, KI-gestützte Frontend-Umsetzung kombiniert mit einem Backend, das mit deinem Business mitwächst.`;

const sideBlocks = [
  { label: '// STANDORT', value: 'Wien, AT' },
  { label: '// ERFAHRUNG', value: '3+ Jahre' },
  { label: '// VERFÜGBAR', value: 'Ab sofort' },
];

const skills = ['Vue.js', 'TypeScript', 'HTML/CSS', 'PHP/SQL', 'Google Sheets API', 'Hosting/Deploy'];

// 3D rotation
const rotateX = ref(-4);
const rotateY = ref(8);
const glareX = ref(50);
const glareY = ref(50);

let animFrame: number;
let isHovering = false;

// Idle floating animation
let idleT = 0;
function idleAnimate() {
  if (!isHovering) {
    idleT += 0.008;
    rotateY.value = Math.sin(idleT) * 10;
    rotateX.value = Math.cos(idleT * 0.7) * 4;
  }
  animFrame = requestAnimationFrame(idleAnimate);
}
idleAnimate();

const glareStyle = computed(() => {
  return `radial-gradient(circle at ${glareX.value}% ${glareY.value}%, rgba(255,255,255,0.15) 0%, transparent 60%)`;
});

function onMouseMove(e: MouseEvent) {
  isHovering = true;
  const el = (e.currentTarget as HTMLElement).querySelector('.card-3d') as HTMLElement;
  if (!el) return;
  const rect = el.getBoundingClientRect();
  const cx = rect.left + rect.width / 2;
  const cy = rect.top + rect.height / 2;
  const dx = (e.clientX - cx) / (rect.width / 2);
  const dy = (e.clientY - cy) / (rect.height / 2);

  rotateY.value = dx * 18;
  rotateX.value = -dy * 12;
  glareX.value = ((e.clientX - rect.left) / rect.width) * 100;
  glareY.value = ((e.clientY - rect.top) / rect.height) * 100;
}

function onMouseLeave() {
  isHovering = false;
}
</script>

<style lang="scss" scoped>
@use "../assets/variables.scss" as *;

$neon: #b4f000;
$blue: #00aaff;
$dark: #0d0d0d;
$card-w: 340px;
$card-h: 520px;

/* ── SECTION ── */
.about-section {
  position: relative;
  width: 100%;
  min-height: 100vh;
  background: $dark;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 80px;
  overflow: hidden;
  padding: 80px 60px;
  box-sizing: border-box;
}

/* ── BACKGROUND ── */
.bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(180, 240, 0, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(180, 240, 0, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  pointer-events: none;
}

.bg-glow {
  position: absolute;
  width: 600px;
  height: 600px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba($neon, 0.06) 0%, transparent 70%);
  top: 50%;
  left: 35%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

/* ── LABEL ── */
.section-label {
  position: absolute;
  top: 50px;
  left: 60px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: $neon;
  letter-spacing: 4px;
  opacity: 0.6;
}

/* ── CARD SCENE ── */
.card-scene {
  flex-shrink: 0;
  width: $card-w;
  height: $card-h;
  filter: drop-shadow(0 30px 60px rgba(0,0,0,0.6)) drop-shadow(0 0 40px rgba($neon, 0.08));
}

.card-3d {
  width: 100%;
  height: 100%;
  transition: transform 0.1s ease-out;
  transform-style: preserve-3d;
  will-change: transform;
}

/* ── CARD FACE ── */
.card-face {
  width: 100%;
  height: 100%;
  border-radius: 20px;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;

  background:
    linear-gradient(135deg, rgba(255,255,255,0.08) 0%, rgba(255,255,255,0.02) 100%);
  border: 1px solid rgba(255,255,255,0.12);
  backdrop-filter: blur(20px);

  // Dark card background
  background-color: #161616;
}

/* ── GLARE ── */
.card-glare {
  position: absolute;
  inset: 0;
  border-radius: 20px;
  pointer-events: none;
  z-index: 10;
  transition: background 0.05s;
}

/* ── CARD TOP ── */
.card-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 22px 14px;

  .card-tag {
    font-family: 'Dogica Pixel', monospace;
    font-size: 8px;
    color: $neon;
    letter-spacing: 2px;
  }

  .card-id {
    font-family: 'Dogica Pixel', monospace;
    font-size: 7px;
    color: #444;
    letter-spacing: 1px;
  }
}

/* ── PHOTO ── */
.card-photo-wrp {
  position: relative;
  width: 110px;
  height: 110px;
  margin: 0 auto 18px;
  flex-shrink: 0;
}

.card-photo {
  width: 110px;
  height: 110px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top;
  display: block;
  border: 3px solid rgba($neon, 0.4);
}

.card-photo-border {
  position: absolute;
  inset: -6px;
  border-radius: 50%;
  border: 1px solid rgba($neon, 0.15);
  animation: spin-border 8s linear infinite;
  background: conic-gradient(from 0deg, rgba($neon, 0.3), transparent 40%, transparent 80%, rgba($neon, 0.3));
}

@keyframes spin-border {
  to { transform: rotate(360deg); }
}

/* ── INFO ── */
.card-info {
  padding: 0 22px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  flex: 1;
}

.info-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgba(255,255,255,0.05);
  padding-bottom: 8px;
}

.info-label {
  font-family: 'Dogica Pixel', monospace;
  font-size: 7px;
  color: #555;
  letter-spacing: 2px;
}

.info-value {
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: #ccc;
  letter-spacing: 1px;

  &.status {
    display: flex;
    align-items: center;
    gap: 6px;
    color: $neon;
  }
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: $neon;
  box-shadow: 0 0 6px $neon;
  animation: pulse-status 2s infinite;
}

@keyframes pulse-status {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.4; }
}

/* ── HOBBIES ── */
.card-hobbies {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  padding: 14px 22px;
}

.hobby-tag {
  font-family: 'Dogica Pixel', monospace;
  font-size: 7px;
  color: #888;
  border: 1px solid #2a2a2a;
  padding: 4px 8px;
  border-radius: 3px;
  letter-spacing: 1px;
  transition: border-color 0.2s, color 0.2s;

  &:hover {
    border-color: rgba($neon, 0.4);
    color: $neon;
  }
}

/* ── BOTTOM BAR ── */
.card-bottom {
  height: 28px;
  background: rgba($neon, 0.08);
  display: flex;
  align-items: center;
  padding: 0 22px;
  gap: 6px;
  border-top: 1px solid rgba($neon, 0.1);
  flex-shrink: 0;
}

.card-stripe {
  height: 10px;
  flex: 1;
  border-radius: 2px;
  background: rgba($neon, 0.15);

  &:nth-child(1) { flex: 2; background: rgba($neon, 0.25); }
  &:nth-child(3) { flex: 0.5; }
}

/* ── SIDE TEXT ── */
.side-text {
  max-width: 380px;
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.side-block {
  animation: fadeInRight 0.6s ease both;

  .side-block-label {
    font-family: 'Dogica Pixel', monospace;
    font-size: 8px;
    color: $neon;
    letter-spacing: 3px;
    margin-bottom: 4px;
    opacity: 0.7;
  }

  .side-block-value {
    font-family: 'Dogica Pixel', monospace;
    font-size: 22px;
    color: white;
    letter-spacing: 2px;
  }
}

@keyframes fadeInRight {
  from { opacity: 0; transform: translateX(20px); }
  to   { opacity: 1; transform: translateX(0); }
}

.about-desc {
  font-family: sans-serif;
  font-size: 14px;
  color: #666;
  line-height: 1.9;
  margin: 0;
}

.skill-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-chip {
  font-family: 'Dogica Pixel', monospace;
  font-size: 8px;
  color: $neon;
  border: 1px solid rgba($neon, 0.25);
  padding: 6px 12px;
  border-radius: 3px;
  letter-spacing: 1px;
  background: rgba($neon, 0.04);
  transition: background 0.2s, border-color 0.2s;

  &:hover {
    background: rgba($neon, 0.1);
    border-color: rgba($neon, 0.6);
  }
}

/* ══════════════ MOBILE ══════════════ */
@media (max-width: 768px) {
  .about-section {
    flex-direction: column;
    gap: 40px;
    padding: 70px 24px 50px;
    min-height: auto;
  }

  .section-label {
    position: static;
    display: block;
    text-align: center;
    margin-bottom: 8px;
  }

  .card-scene {
    width: 260px;
    height: 400px;
  }

  .side-text {
    max-width: 100%;
    text-align: center;
    align-items: center;
  }

  .side-block {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .skill-chips {
    justify-content: center;
  }
}
</style>