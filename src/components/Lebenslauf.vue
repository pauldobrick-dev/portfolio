<template>
  <div class="lebenslauf-wrp">
    <div class="title-wrp">
      <span class="title-label">// CURRICULUM VITAE</span>
      <h2 class="title">Werdegang</h2>
    </div>
 
    <div class="timeline" ref="timelineRef">
      <div class="timeline-line"></div>
 
      <!-- LEFT SIDE ITEMS -->
      <div
        v-for="(item, index) in leftItems"
        :key="item.id"
        class="timeline-item left"
        :class="{ visible: visible, active: hoveredId === item.id }"
        :style="{ animationDelay: `${index * 0.2}s` }"
        @mouseenter="hoveredId = item.id"
        @mouseleave="hoveredId = null"
      >
        <div class="item-content">
          <div class="item-year">{{ item.year }}</div>
          <div class="item-title" :style="item.color ? { color: item.color } : {}">{{ item.title }}</div>
          <div class="item-sub">{{ item.sub }}</div>
        </div>
        <div class="connector">
          <div class="connector-line"></div>
          <div class="dot"></div>
        </div>
      </div>
 
      <!-- RIGHT SIDE ITEMS -->
      <div
        v-for="(item, index) in rightItems"
        :key="item.id"
        class="timeline-item right"
        :class="{ visible: visible, active: hoveredId === item.id }"
        :style="{ animationDelay: `${(index + leftItems.length) * 0.2}s` }"
        @mouseenter="hoveredId = item.id"
        @mouseleave="hoveredId = null"
      >
        <div class="connector">
          <div class="dot"></div>
          <div class="connector-line"></div>
        </div>
        <div class="item-content">
          <div class="item-year">{{ item.year }}</div>
          <div class="item-title" :style="item.color ? { color: item.color } : {}">{{ item.title }}</div>
          <div class="item-sub">{{ item.sub }}</div>
        </div>
      </div>
 
      <!-- JETZT Marker -->
      <div class="now-marker">
        <div class="now-dot"></div>
        <span>{{ currentMonthYear }}</span>
      </div>
 
    </div>
  </div>
</template>
 
<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
 
const hoveredId = ref<string | null>(null);

const MONTHS_DE = [
  'Januar', 'Februar', 'März', 'April', 'Mai', 'Juni',
  'Juli', 'August', 'September', 'Oktober', 'November', 'Dezember',
];

const currentMonthYear = computed(() => {
  const now = new Date();
  return `${MONTHS_DE[now.getMonth()]}, ${now.getFullYear()}`;
});
 
const leftItems = [
  {
    id: 'l2',
    year: '2022 – 2024',
    title: 'BERUFSKOLLEG OLSBERG DES HSK',
    sub: 'Schulische Ausbildung + Fachabitur zum\n"Informationstechnischen Assistent"',
    color: '',
  },
  {
    id: 'l3',
    year: '2024 – 2026',
    title: 'BERUFSKOLLEG OLSBERG DES HSK',
    sub: 'Fachoberschulreife – Naturwissenschaften',
    color: '',
  },
];
 
const rightItems = [
  {
    id: 'r1',
    year: '2022 – 2023',
    title: 'RICHTER ELEKTRONIK',
    sub: '8 Wöchiges Praktikum\n+ Facharbeit',
    color: '',
  },
  {
    id: 'r2',
    year: '2023 – 2026',
    title: 'RICHTER ELEKTRONIK',
    sub: 'Minijob',
    color: '',
  },
    {
    id: 'r3',
    year: 'vsl. 2026 - 2029',
    title: 'TU Wien',
    sub: 'Bsc. Technische Informatik',
    color: '#b4f000',
  },
  
];
 
const timelineRef = ref<HTMLElement | null>(null);
const visible = ref(false);
 
onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry?.isIntersecting) {
        visible.value = true;
      }
    },
    { threshold: 0.1 }
  );
 
  if (timelineRef.value) {
    observer.observe(timelineRef.value);
  }
});
</script>
 
<style lang="scss" scoped>
@use "../assets/variables.scss" as *;
 
$neon: #b4f000;
$dark: #111111;
$mid: #1a1a1a;
$dim: #333;
$text-muted: #555;
 
.lebenslauf-wrp {
  width: 100%;
  min-height: 100vh;
  background-color: $dark;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 60px 0 100px;
  box-sizing: border-box;
  overflow: hidden;
}
 
/* ── TITLE ── */
.title-wrp {
  text-align: center;
  margin-bottom: 60px;
 
  .title-label {
    font-family: 'Dogica Pixel', monospace;
    font-size: 10px;
    color: $neon;
    letter-spacing: 4px;
    opacity: 0.7;
  }
 
  .title {
    font-family: 'Dogica Pixel', monospace;
    font-size: clamp(28px, 4vw, 52px);
    color: white;
    margin: 8px 0 0;
    letter-spacing: 6px;
  }
}
 
/* ── TIMELINE WRAPPER ── */
.timeline {
  position: relative;
  width: 90%;
  max-width: 1100px;
  display: grid;
  grid-template-columns: 1fr 2px 1fr;
  row-gap: 0;
}
 
/* ── CENTER LINE ── */
.timeline-line {
  grid-column: 2;
  grid-row: 1 / 99;
  width: 2px;
  background: linear-gradient(to bottom, transparent, $dim 10%, $dim 90%, transparent);
  justify-self: center;
}
 
/* ── NOW MARKER ── */
.now-marker {
  grid-column: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  padding: 20px 0 0;
  z-index: 10;
 
  .now-dot {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: $neon;
    box-shadow: 0 0 16px $neon, 0 0 32px rgba($neon, 0.4);
    animation: pulse-dot 2s infinite ease-in-out;
  }
 
  span {
    font-family: 'Dogica Pixel', monospace;
    font-size: 11px;
    color: white;
    white-space: nowrap;
    opacity: 0.8;
    letter-spacing: 2px;
  }
}
 
@keyframes pulse-dot {
  0%, 100% { box-shadow: 0 0 10px $neon, 0 0 20px rgba($neon, 0.3); }
  50%       { box-shadow: 0 0 20px $neon, 0 0 50px rgba($neon, 0.6); }
}
 
/* ── TIMELINE ITEM ── */
.timeline-item {
  position: relative;
  display: flex;
  align-items: center;
  padding: 30px 0;
  cursor: pointer;
 
  /* Startzustand für Scroll-Animation */
  opacity: 0;
  transform: translateY(30px);
 
  &.visible {
    animation: fadeInUp 0.6s ease forwards;
  }
 
  &.left {
    grid-column: 1;
    justify-content: flex-end;
    padding-right: 0;
 
    .item-content {
      text-align: right;
      padding-right: 28px;
    }
  }
 
  &.right {
    grid-column: 3;
    justify-content: flex-start;
    padding-left: 0;
 
    .item-content {
      text-align: left;
      padding-left: 28px;
    }
  }
}
 
@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
 
/* ── CONNECTOR ── */
.connector {
  display: flex;
  align-items: center;
  flex-shrink: 0;
 
  .connector-line {
    width: 30px;
    height: 1px;
    background: $dim;
    transition: background 0.3s;
  }
 
  .dot {
    position: relative;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    border: 2px solid $dim;
    background: $dark;
    flex-shrink: 0;
    transition: border-color 0.3s, box-shadow 0.3s;
  }
}
 
.timeline-item.left .connector {
  flex-direction: row-reverse;
}
 
.timeline-item:hover .dot {
  border-color: $neon;
  box-shadow: 0 0 8px $neon;
}
 
.timeline-item:hover .connector-line {
  background: $neon;
}
 
/* ── ITEM CONTENT ── */
.item-content {
  max-width: 320px;
}
 
.item-year {
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: $text-muted;
  letter-spacing: 2px;
  margin-bottom: 6px;
  transition: color 0.3s;
}
 
.item-title {
  font-family: 'Dogica Pixel', monospace;
  font-size: clamp(10px, 1.1vw, 13px);
  color: #ccc;
  letter-spacing: 1px;
  line-height: 1.5;
  transition: color 0.3s;
  white-space: pre-line;
}
 
.item-sub {
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: $text-muted;
  margin-top: 6px;
  line-height: 1.7;
  white-space: pre-line;
  transition: color 0.3s;
}
 
.timeline-item:hover .item-year,
.timeline-item:hover .item-sub {
  color: #888;
}
 
.timeline-item:hover .item-title {
  color: white;
}

@media (max-width: 700px) {
  .timeline {
    width: 100%;
    max-width: 480px;
    grid-template-columns: 1fr;
    padding: 0 20px;
    box-sizing: border-box;
  }

  .timeline-line { display: none; }

  .timeline-item.left,
  .timeline-item.right {
    grid-column: 1;
    justify-content: flex-start;
    padding: 22px 0 22px 20px;
    border-left: 2px solid $dim;
  }

  .timeline-item.left .item-content,
  .timeline-item.right .item-content {
    text-align: left;
    padding-left: 18px;
    padding-right: 0;
    max-width: 100%;
  }

  .timeline-item .connector { display: none; }

  .now-marker {
    grid-column: 1;
    align-items: flex-start;
    padding-left: 18px;
  }
}
</style>