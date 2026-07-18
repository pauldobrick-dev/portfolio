<template>
  <Transition name="modal-fade">
    <div class="modal-backdrop" @click.self="close">
      <div class="modal-card">

        <button class="modal-close" @click="close" aria-label="Schließen">✕</button>

        <div class="modal-label">// ANFRAGE</div>
        <h3 class="modal-title">Kontakt aufnehmen</h3>
        <p class="modal-sub">
          Kurz Kontaktdaten und Anliegen eintragen — ich melde mich in der Regel
          innerhalb von 24 Stunden zurück.
        </p>

        <!-- ERFOLGS-STATE -->
        <div v-if="status === 'success'" class="status-box success">
          <span class="status-icon">✓</span>
          <div>
            <strong>Danke für deine Anfrage!</strong>
            <p>Ich melde mich schnellstmöglich bei dir zurück.</p>
          </div>
        </div>

        <!-- FEHLER-STATE -->
        <div v-if="status === 'error'" class="status-box error">
          <span class="status-icon">!</span>
          <div>
            <strong>Da ist etwas schiefgelaufen.</strong>
            <p>Bitte versuch es nochmal oder schreib mir direkt eine E-Mail.</p>
          </div>
        </div>

        <!-- FORMULAR -->
        <form v-if="status !== 'success'" @submit.prevent="submitForm" class="contact-form">

          <label class="field">
            <span class="field-label">NAME *</span>
            <input v-model="form.name" type="text" required placeholder="Dein Name" />
          </label>

          <label class="field">
            <span class="field-label">E-MAIL *</span>
            <input v-model="form.email" type="email" required placeholder="deine@email.at" />
          </label>

          <label class="field">
            <span class="field-label">TELEFONNUMMER</span>
            <input v-model="form.phone" type="tel" placeholder="Optional" />
          </label>

          <label class="field">
            <span class="field-label">ANLIEGEN *</span>
            <select v-model="form.reason" required>
              <option disabled value="">Bitte auswählen</option>
              <option>Website-Check</option>
              <option>Neue Website</option>
              <option>Website-Überarbeitung</option>
              <option>Sonstiges</option>
            </select>
          </label>

          <label class="field">
            <span class="field-label">NACHRICHT</span>
            <textarea v-model="form.message" rows="4" placeholder="Kurz erzählen, worum es geht..."></textarea>
          </label>

          <button type="submit" class="submit-btn" :disabled="status === 'sending'">
            {{ status === 'sending' ? 'Wird gesendet...' : 'Anfrage senden' }}
          </button>

        </form>

      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
import { reactive, ref, watch } from 'vue';

const props = defineProps<{
  initialReason?: string;
}>();

const emit = defineEmits<{
  (e: 'close'): void;
}>();

// TODO: Formspree-Formular unter https://formspree.io kostenlos anlegen
// und die Endpoint-ID hier eintragen (Format: https://formspree.io/f/xxxxxxxx)
const FORMSPREE_ENDPOINT = 'https://formspree.io/f/xwvgopad';

const form = reactive({
  name: '',
  email: '',
  phone: '',
  reason: props.initialReason ?? '',
  message: '',
});

// Falls das Modal für ein anderes Paket erneut geöffnet wird, Anliegen nachziehen
watch(() => props.initialReason, (val) => {
  if (val) form.reason = val;
});

const status = ref<'idle' | 'sending' | 'success' | 'error'>('idle');

async function submitForm() {
  status.value = 'sending';
  try {
    const res = await fetch(FORMSPREE_ENDPOINT, {
      method: 'POST',
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        name: form.name,
        email: form.email,
        phone: form.phone,
        reason: form.reason,
        message: form.message,
      }),
    });

    if (res.ok) {
      status.value = 'success';
    } else {
      status.value = 'error';
    }
  } catch (err) {
    status.value = 'error';
  }
}

function close() {
  emit('close');
}
</script>

<style lang="scss" scoped>
@use "../assets/variables.scss" as *;

$neon: #b4f000;
$dark: #111111;
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
  max-width: 440px;
  max-height: 90vh;
  overflow-y: auto;
  background-color: $card-bg;
  border: 1px solid rgba($neon, 0.3);
  border-radius: 12px;
  padding: 36px 32px;
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
  font-size: 22px;
  color: white;
  letter-spacing: 2px;
  margin: 0 0 10px;
}

.modal-sub {
  font-family: sans-serif;
  font-size: 13px;
  color: #888;
  line-height: 1.6;
  margin: 0 0 26px;
}

/* ── STATUS BOXES ── */
.status-box {
  display: flex;
  gap: 14px;
  align-items: flex-start;
  padding: 18px;
  border-radius: 8px;
  margin-bottom: 8px;

  strong {
    font-family: 'Dogica Pixel', monospace;
    font-size: 11px;
    color: white;
    letter-spacing: 1px;
  }

  p {
    font-family: sans-serif;
    font-size: 13px;
    color: #999;
    margin: 6px 0 0;
    line-height: 1.5;
  }

  .status-icon {
    flex-shrink: 0;
    width: 26px;
    height: 26px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 13px;
    font-weight: bold;
  }

  &.success {
    background: rgba($neon, 0.08);
    border: 1px solid rgba($neon, 0.3);

    .status-icon {
      background: $neon;
      color: #111;
    }
  }

  &.error {
    background: rgba(#ff4444, 0.08);
    border: 1px solid rgba(#ff4444, 0.3);

    .status-icon {
      background: #ff4444;
      color: white;
    }
  }
}

/* ── FORM ── */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.field-label {
  font-family: 'Dogica Pixel', monospace;
  font-size: 8px;
  color: #777;
  letter-spacing: 2px;
}

input,
select,
textarea {
  font-family: sans-serif;
  font-size: 14px;
  color: #eee;
  background: #0d0d0d;
  border: 1px solid $dim;
  border-radius: 6px;
  padding: 12px 14px;
  outline: none;
  transition: border-color 0.2s;
  resize: vertical;

  &:focus {
    border-color: rgba($neon, 0.6);
  }

  &::placeholder {
    color: #555;
  }
}

select {
  cursor: pointer;
}

.submit-btn {
  margin-top: 6px;
  font-family: 'Dogica Pixel', monospace;
  font-size: 11px;
  letter-spacing: 1px;
  color: #111;
  background: $neon;
  border: none;
  padding: 15px 0;
  border-radius: 6px;
  cursor: pointer;
  transition: filter 0.2s, transform 0.2s;

  &:hover:not(:disabled) {
    filter: brightness(1.08);
    transform: translateY(-1px);
  }

  &:disabled {
    opacity: 0.6;
    cursor: not-allowed;
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
    padding: 28px 22px;
  }
}
</style>