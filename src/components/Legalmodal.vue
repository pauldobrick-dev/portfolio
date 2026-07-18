<template>
  <Transition name="modal-fade">
    <div class="modal-backdrop" @click.self="close">
      <div class="modal-card">

        <button class="modal-close" @click="close" aria-label="Schließen">✕</button>

        <div class="modal-label">// {{ type === 'impressum' ? 'IMPRESSUM' : 'DATENSCHUTZ' }}</div>
        <h3 class="modal-title">{{ type === 'impressum' ? 'Impressum' : 'Datenschutzerklärung' }}</h3>

        <!-- ═══════════════ IMPRESSUM ═══════════════ -->
        <div v-if="type === 'impressum'" class="legal-body">
          <!--<p class="placeholder-warning">
            ⚠ Platzhalter mit [ ] noch ausfüllen, sobald die Gewerbeanmeldung
            abgeschlossen ist (GISA-Zahl etc.).
          </p>-->

          <h4>Angaben gemäß § 5 ECG, § 25 Mediengesetz</h4>
          <p>
            Paul Dobrick<br>
            Lambrechtgasse 16 / Top 29<br>
            1040 Wien, Österreich
          </p>

          <h4>Kontakt</h4>
          <p>
            E-Mail: paul.dobrick@outlook.de<br>
            Telefon: +49 160 95730366
          </p>

          <h4>Unternehmensgegenstand</h4>
          <p>Dienstleistungen in der automatischen Datenverarbeitung und Informationstechnik</p>

          <h4>Gewerbebehörde</h4>
          <p>Magistratisches Bezirksamt für den 4. und 5. Bezirk, Wien</p>

          <h4>GISA-Zahl</h4>
          <p>[folgt nach Abschluss der Gewerbeanmeldung]</p>

          <h4>Mitgliedschaft</h4>
          <p>Wirtschaftskammer Wien, Fachgruppe UBIT (Unternehmensberatung, Buchhaltung und Informationstechnologie)</p>

          <h4>Anwendbare Rechtsvorschriften</h4>
          <p>Gewerbeordnung: <a href="https://www.ris.bka.gv.at" target="_blank" rel="noopener">www.ris.bka.gv.at</a></p>

          <h4>Umsatzsteuer</h4>
          <p>Kleinunternehmer gemäß § 6 Abs. 1 Z 27 UStG — keine Umsatzsteuer ausgewiesen.</p>

          <h4>EU-Streitschlichtung</h4>
          <p>
            Die Europäische Kommission stellt eine Plattform zur Online-Streitbeilegung bereit:
            <a href="https://ec.europa.eu/consumers/odr" target="_blank" rel="noopener">ec.europa.eu/consumers/odr</a>.
            Ich bin nicht verpflichtet und nicht bereit, an einem Streitbeilegungsverfahren
            vor einer Verbraucherschlichtungsstelle teilzunehmen.
          </p>

          <h4>Haftung für Links</h4>
          <p>
            Diese Website enthält Links zu externen Seiten Dritter, auf deren Inhalte
            kein Einfluss besteht. Für diese fremden Inhalte wird keine Gewähr übernommen.
          </p>
        </div>

        <!-- ═══════════════ DATENSCHUTZ ═══════════════ -->
        <div v-else class="legal-body">
          <!--<p class="placeholder-warning">
            ⚠ Platzhalter mit [ ] noch ausfüllen bzw. an dein finales Setup
            (Hosting-Anbieter, evtl. Formular-Dienst) anpassen.
          </p>-->

          <h4>1. Verantwortlicher</h4>
          <p>
            Paul Dobrick, Lambrechtgasse 16, 1040 Wien<br>
            E-Mail: paul.dobrick@outlook.de
          </p>

          <h4>2. Kontaktformular</h4>
          <p>
            Wenn du das Kontaktformular auf dieser Website nutzt, werden die von dir
            eingegebenen Daten (Name, E-Mail-Adresse, optional Telefonnummer, Anliegen,
            Nachricht) zur Bearbeitung deiner Anfrage verarbeitet. Rechtsgrundlage ist
            Art. 6 Abs. 1 lit. b DSGVO (vorvertragliche Maßnahmen bzw. Vertragsanbahnung).
          </p>
          <p>
            Zur technischen Abwicklung wird der Formular-Dienst <strong>Formspree</strong>
            (Formspree, Inc., USA) eingesetzt. Dabei kann es zu einer Datenübermittlung
            in ein Drittland (USA) kommen. Formspree verwendet nach eigenen Angaben
            geeignete Garantien (u. a. Standardvertragsklauseln). Details dazu findest
            du in der Datenschutzerklärung von Formspree:
            <a href="https://formspree.io/legal/privacy-policy/" target="_blank" rel="noopener">
              formspree.io/legal/privacy-policy
            </a>.
          </p>

          <h4>3. Speicherdauer</h4>
          <p>
            Deine Angaben werden nur so lange gespeichert, wie es zur Bearbeitung
            deiner Anfrage erforderlich ist, danach werden sie gelöscht, sofern keine
            gesetzliche Aufbewahrungspflicht entgegensteht.
          </p>

          <h4>4. Hosting</h4>
          <p>
            Beim Aufruf dieser Website werden durch den Hosting-Anbieter automatisch
            technische Daten (z. B. IP-Adresse, Datum/Uhrzeit des Zugriffs) in
            sogenannten Server-Logfiles erfasst. Dies dient der technischen
            Bereitstellung und Sicherheit der Website. [Hosting-Anbieter hier ergänzen,
            z. B. Netlify/Vercel — inkl. Link zu dessen Datenschutzerklärung.]
          </p>

          <h4>5. Deine Rechte</h4>
          <p>
            Du hast das Recht auf Auskunft, Berichtigung, Löschung, Einschränkung der
            Verarbeitung, Datenübertragbarkeit sowie Widerspruch gegen die Verarbeitung
            deiner personenbezogenen Daten. Wende dich dazu einfach an die oben
            genannte Kontakt-E-Mail-Adresse.
          </p>
          <p>
            Außerdem hast du das Recht, dich bei der österreichischen Datenschutzbehörde
            zu beschweren: Österreichische Datenschutzbehörde, Barichgasse 40–42,
            1030 Wien, <a href="https://www.dsb.gv.at" target="_blank" rel="noopener">www.dsb.gv.at</a>.
          </p>

          <h4>6. Cookies</h4>
          <p>
            Diese Website setzt aktuell keine Analyse- oder Marketing-Cookies ein.
            Falls sich das ändert (z. B. durch Analyse-Tools), wird diese Erklärung
            entsprechend aktualisiert.
          </p>
        </div>

      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
defineProps<{
  type: 'impressum' | 'datenschutz';
}>();

const emit = defineEmits<{
  (e: 'close'): void;
}>();

function close() {
  emit('close');
}
</script>

<style lang="scss" scoped>
@use "../assets/variables.scss" as *;

$neon: #b4f000;
$card-bg: #161616;
$dim: #2a2a2a;

.modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
}

.modal-card {
  position: relative;
  width: 100%;
  max-width: 620px;
  max-height: 85vh;
  overflow-y: auto;
  background-color: $card-bg;
  border: 1px solid rgba($neon, 0.3);
  border-radius: 12px;
  padding: 36px 32px 40px;
  box-shadow: 0 30px 80px rgba(0,0,0,0.5), 0 0 40px rgba($neon, 0.08);
}

.modal-close {
  position: absolute;
  top: 18px;
  right: 18px;
  background: transparent;
  border: 1px solid $dim;
  color: #888;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 13px;
  transition: border-color 0.2s, color 0.2s;

  &:hover {
    border-color: $neon;
    color: $neon;
  }
}

.modal-label {
  font-family: 'Dogica Pixel', monospace;
  font-size: 9px;
  color: $neon;
  letter-spacing: 3px;
  opacity: 0.75;
  margin-bottom: 8px;
}

.modal-title {
  font-family: 'Dogica Pixel', monospace;
  font-size: 20px;
  color: white;
  letter-spacing: 1px;
  margin: 0 0 22px;
}

.placeholder-warning {
  font-family: sans-serif;
  font-size: 12px;
  color: #d9a44e;
  background: rgba(#d9a44e, 0.08);
  border: 1px solid rgba(#d9a44e, 0.3);
  border-radius: 6px;
  padding: 10px 14px;
  margin-bottom: 24px;
  line-height: 1.5;
}

.legal-body {
  font-family: sans-serif;
  font-size: 13.5px;
  color: #bbb;
  line-height: 1.7;

  h4 {
    font-family: 'Dogica Pixel', monospace;
    font-size: 10px;
    color: $neon;
    letter-spacing: 1px;
    margin: 22px 0 8px;

    &:first-child {
      margin-top: 0;
    }
  }

  p {
    margin: 0 0 4px;
  }

  a {
    color: #6ec8ff;
    text-decoration: none;
    border-bottom: 1px solid rgba(#6ec8ff, 0.3);

    &:hover {
      border-color: #6ec8ff;
    }
  }

  strong {
    color: #ddd;
  }
}

/* ── TRANSITION ── */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.25s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

/* ── MOBILE ── */
@media (max-width: 480px) {
  .modal-card {
    padding: 28px 22px 32px;
  }
}
</style>