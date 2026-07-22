<template>
  <div class="packages-section" ref="sectionRef">

    <div class="bg-grid"></div>

    <div class="title-wrp">
      <span class="title-label">// LEISTUNGEN</span>
      <h2 class="title">WAS ICH ANBIETE</h2>
      <p class="title-sub">
        Individuelle Websites für Unternehmen — vom kostenlosen Check bis zur
        vollständigen Business-Lösung mit eigenem Backend.
      </p>
    </div>

    <div class="packages-grid">
      <div
        v-for="(pkg, i) in packages"
        :key="pkg.id"
        class="package-card"
        :class="{ visible, featured: pkg.featured }"
        :style="{ animationDelay: `${i * 0.15}s` }"
      >
        <div v-if="pkg.featured" class="featured-badge">BELIEBT</div>

        <div class="pkg-name">{{ pkg.name }}</div>
        <div class="pkg-price">
          <span class="price-prefix" v-if="pkg.pricePrefix">{{ pkg.pricePrefix }}</span>
          <span class="price-value">{{ pkg.price }}</span>
        </div>
        <div class="pkg-sub">{{ pkg.subtitle }}</div>

        <ul class="pkg-features">
          <li v-for="feat in pkg.features" :key="feat">
            <span class="feat-check">✓</span>{{ feat }}
          </li>
        </ul>

        <button class="pkg-cta" @click="$emit('open-contact', pkg.reason)">
          {{ pkg.ctaLabel }}
        </button>
      </div>
    </div>

    <p class="packages-note">
      Jedes Projekt ist unterschiedlich — die Preise oben sind Richtwerte.
      Nach einem kurzen, unverbindlichen Gespräch bekommst du ein genaues Angebot.
    </p>

  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const sectionRef = ref<HTMLElement | null>(null);
const visible = ref(false);

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry?.isIntersecting) visible.value = true;
    },
    { threshold: 0.15 }
  );
  if (sectionRef.value) observer.observe(sectionRef.value);
});

const emit = defineEmits<{
  (e: 'open-contact', reason: string): void;
}>();

const packages = [
  {
    id: 'check',
    name: 'Website-Check',
    price: 'Kostenlos',
    pricePrefix: '',
    subtitle: 'Der unverbindliche erste Schritt',
    features: [
      'Kurze Analyse deiner bestehenden Website (oder Online-Präsenz)',
      '2–3 konkrete Verbesserungsvorschläge',
      'Kein Risiko, keine Verpflichtung',
    ],
    ctaLabel: 'Check anfragen',
    reason: 'Website-Check',
    featured: false,
  },
  {
    id: 'starter',
    name: 'Starter-Website',
    price: '800 €',
    pricePrefix: 'ab',
    subtitle: 'Für den professionellen Auftritt',
    features: [
      '1–5 Seiten, individuell gestaltet',
      'Responsive für Mobile, Tablet & Desktop',
      'Kontaktformular & Basis-SEO',
      'Hosting-Einrichtung inklusive',
    ],
    ctaLabel: 'Anfragen',
    reason: 'Neue Website',
    featured: true,
  },
  {
    id: 'business',
    name: 'Business-Website',
    price: '2000 €',
    pricePrefix: 'ab',
    subtitle: 'Mit eigenem, wachsendem Backend',
    features: [
      'Alles aus dem Starter-Paket',
      'Individuelles Backend (z. B. Events, Inhalte selbst pflegen)',
      'Self-Service ohne Code-Kenntnisse für dich als Kunde',
      'Einschulung & Support beim Start',
    ],
    ctaLabel: 'Anfragen',
    reason: 'Neue Website',
    featured: false,
  },
];
</script>

<style lang="scss" scoped>
@use "../assets/variables.scss" as *;

$neon: #b4f000;
$blue: #00aaff;
$dark: #111111;
$card-bg: #161616;
$dim: #2a2a2a;
$text-muted: #666;

.packages-section {
  position: relative;
  width: 100%;
  min-height: 100vh;
  background-color: $dark;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 90px 60px 100px;
  box-sizing: border-box;
  overflow: hidden;
}

.bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba($neon, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba($neon, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  pointer-events: none;
}

/* ── TITLE ── */
.title-wrp {
  position: relative;
  text-align: center;
  margin-bottom: 64px;
  max-width: 560px;

  .title-label {
    font-family: 'Dogica Pixel', monospace;
    font-size: 10px;
    color: $neon;
    letter-spacing: 4px;
    opacity: 0.7;
  }

  .title {
    font-family: 'Dogica Pixel', monospace;
    font-size: clamp(28px, 4vw, 48px);
    color: white;
    margin: 8px 0 18px;
    letter-spacing: 5px;
  }

  .title-sub {
    font-family: sans-serif;
    font-size: 14px;
    color: #777;
    line-height: 1.7;
    margin: 0;
  }
}

/* ── GRID ── */
.packages-grid {
  position: relative;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  width: 100%;
  max-width: 1080px;

  @media (max-width: 900px) {
    grid-template-columns: 1fr;
    max-width: 420px;
  }
}

/* ── CARD ── */
.package-card {
  position: relative;
  background-color: $card-bg;
  border: 1px solid $dim;
  border-radius: 10px;
  padding: 32px 26px;
  display: flex;
  flex-direction: column;
  opacity: 0;
  transform: translateY(24px);
  transition: border-color 0.3s, transform 0.3s;

  &.visible {
    animation: fadeInUp 0.6s ease forwards;
  }

  &:hover {
    border-color: rgba($neon, 0.4);
    transform: translateY(-4px);
  }

  &.featured {
    border-color: rgba($neon, 0.5);
    background: linear-gradient(180deg, rgba($neon, 0.04), $card-bg 40%);

    &:hover {
      transform: translateY(-6px);
    }
  }
}

@keyframes fadeInUp {
  to { opacity: 1; transform: translateY(0); }
}

.featured-badge {
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%);
  background: $neon;
  color: #111;
  font-family: 'Dogica Pixel', monospace;
  font-size: 8px;
  letter-spacing: 2px;
  padding: 5px 14px;
  border-radius: 20px;
}

.pkg-name {
  font-family: 'Dogica Pixel', monospace;
  font-size: 13px;
  color: white;
  letter-spacing: 1px;
  margin-bottom: 14px;
}

.pkg-price {
  display: flex;
  align-items: baseline;
  gap: 6px;
  margin-bottom: 6px;

  .price-prefix {
    font-family: 'Dogica Pixel', monospace;
    font-size: 10px;
    color: $text-muted;
  }

  .price-value {
    font-family: 'Dogica Pixel', monospace;
    font-size: 26px;
    color: $neon;
    letter-spacing: 1px;
  }
}

.pkg-sub {
  font-family: sans-serif;
  font-size: 12px;
  color: #777;
  margin-bottom: 22px;
}

.pkg-features {
  list-style: none;
  margin: 0 0 26px;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
  flex: 1;

  li {
    display: flex;
    align-items: flex-start;
    gap: 8px;
    font-family: sans-serif;
    font-size: 12.5px;
    color: #aaa;
    line-height: 1.5;
  }

  .feat-check {
    color: $neon;
    font-size: 11px;
    margin-top: 2px;
    flex-shrink: 0;
  }
}

.pkg-cta {
  width: 100%;
  font-family: 'Dogica Pixel', monospace;
  font-size: 10px;
  letter-spacing: 1px;
  color: #ccc;
  background: transparent;
  border: 1px solid $dim;
  padding: 14px 0;
  border-radius: 6px;
  cursor: pointer;
  transition: border-color 0.2s, color 0.2s, background 0.2s;

  &:hover {
    border-color: $neon;
    color: $neon;
    background: rgba($neon, 0.06);
  }
}

.package-card.featured .pkg-cta {
  color: #111;
  background: $neon;
  border-color: $neon;

  &:hover {
    filter: brightness(1.08);
  }
}

/* ── NOTE ── */
.packages-note {
  margin-top: 44px;
  max-width: 560px;
  text-align: center;
  font-family: sans-serif;
  font-size: 12px;
  color: #555;
  line-height: 1.7;
}
</style>