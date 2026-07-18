<template>
  <div class="next-section-wrp" id="home">
    <Hero @open-contact="openContact" />
  </div>

  <div class="next-section-wrp" id="projects">
    <Projects @open-contact="openContact" />
  </div>
  <div class="next-section-wrp packages-wrp" id="packages">
    <Packages @open-contact="openContact" />
  </div>
  <div class="next-section-wrp" id="lebenslauf">
    <Lebenslauf />
  </div>
  <div class="next-section-wrp" id="about">
    <AboutMe />
  </div>

  <div class="footer-wrp">
    <Footer @open-legal="openLegal" />
  </div>

  <ContactModal
    v-if="contactOpen"
    :initial-reason="contactReason"
    @close="contactOpen = false"
  />

  <LegalModal
    v-if="legalOpen"
    :type="legalType"
    @close="legalOpen = false"
  />
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import Hero from "./components/Hero.vue";
import Lebenslauf from "./components/Lebenslauf.vue";
import Projects from "./components/Projects.vue";
import Packages from "./components/Packages.vue";
import AboutMe from "./components/AboutMe.vue";
import ContactModal from "./components/ContactModal.vue";
import Footer from "./components/Footer.vue";
import LegalModal from "./components/LegalModal.vue";

onMounted(() => {
  document.title = "Paul Dobrick | Portfolio";
});

const contactOpen = ref(false);
const contactReason = ref("");

function openContact(reason: string) {
  contactReason.value = reason;
  contactOpen.value = true;
}

const legalOpen = ref(false);
const legalType = ref<'impressum' | 'datenschutz'>('impressum');

function openLegal(type: 'impressum' | 'datenschutz') {
  legalType.value = type;
  legalOpen.value = true;
}
</script>

<style lang="scss">
@use "./assets/variables.scss" as *;

/* Ohne diesen Reset zählt der Browser bei width:100% + padding das Padding
   zusätzlich zur Breite dazu — das lässt viele Komponenten (Sidebar,
   Hero-Content, Package-Cards etc.) minimal breiter als den Bildschirm
   werden und erzeugt genau den weißen Rand rechts auf Mobile. */
*, *::before, *::after {
  box-sizing: border-box;
}

html {
  scroll-snap-type: y mandatory;
  scroll-behavior: smooth;
}

body {
  padding: 0;
  margin: 0;
  font-family: 'Dogica Pixel', monospace;
  overflow-x: hidden;
  background-color: #111111;
}

.next-section-wrp {
  height: 100vh;
  width: 100%;
  scroll-snap-align: start;
  position: relative;
  overflow: hidden;
}

/* Packages hat 3 Karten + Titel + Hinweistext — auf kleineren Screens
   ggf. höher als 100vh. Erlaubt hier vertikales Scrollen innerhalb der
   Sektion, statt Inhalt abzuschneiden. */
.packages-wrp {
  height: auto;
  min-height: 100vh;
  overflow-y: auto;
}

/* Footer: eigener Snap-Punkt, aber natürliche Höhe statt 100vh — sonst
   würde das mandatory Snapping verhindern, dass man dort zum Stehen kommt. */
.footer-wrp {
  scroll-snap-align: start;
}

/* ══════════════ MOBILE ══════════════
   Auf schmalen Screens wird gestapelter Content (Hero, About, Timeline etc.)
   oft höher als exakt 100vh. Scroll-Snap + feste Höhe + overflow:hidden
   würde dann Inhalte abschneiden — deshalb hier global aufgehoben. */
@media (max-width: 768px) {
  html {
    scroll-snap-type: none;
  }

  .next-section-wrp {
    height: auto;
    min-height: 100vh;
    overflow: visible;
  }
}
</style>