<template>
  <div>
    <!-- <NumberInput v-model="fkValue" placeholder="FK-Wert"></NumberInput> -->
    <div class="row">
      <div class="col-2">
        <CheckboxInput v-model="dämmerungssicht">Dämmerungssicht</CheckboxInput>
        <CheckboxInput v-model="nachtsicht">Nachtsicht</CheckboxInput>
      </div>
      <div class="col-2"></div>
      <div class="col-2"></div>
      <div class="col-2"></div>
      <div class="col-2"></div>
      <div class="col-2"></div>
    </div>
    <div class="row">
      <div class="col-2">
        <SelectInput
          :options="Object.entries(DISTANCE)"
          :option-projection="(e) => e[0]"
          show-all
          @select-item="(e) => (distance = e)"
        ></SelectInput>
      </div>
      <div class="col-2">
        <SelectInput
          :options="Object.entries(MOVEMENT)"
          :option-projection="(e) => e[0]"
          show-all
          @select-item="(e) => (movement = e)"
        ></SelectInput>
      </div>
      <div class="col-2">
        <SelectInput
          :options="Object.entries(SIGHT)"
          :option-projection="(e) => e[0]"
          show-all
          @select-item="(e) => (sight = e)"
        ></SelectInput>
      </div>
      <div class="col-2">{{ fkValue }}</div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { CheckboxInput, NumberInput, SelectInput } from "custom-mbd-components";
import { computed, ref } from "vue";

const fkValue = computed(
  () =>
    (-distance.value[1] || 0) -
    (movement.value[1] || 0) -
    (nachtsicht.value
      ? Math.round((sight.value[1] || 0) / 2)
      : sight.value[1] - +(sight.value[0] == "Dämmerung") || 0)
);
const distance = ref([]);
const movement = ref([]);
const sight = ref([]);
const dämmerungssicht = ref(false);
const nachtsicht = ref(false);
const nachtblind = ref(false);

function sightValue() {}

const DISTANCE = {
  "sehr nah": -2,
  nah: 0,
  mittel: 4,
  weit: 8,
  "sehr weit": 12,
};

const MOVEMENT = {
  "fest/unbeweglich": -4,
  stillstehend: -2,
  "leicht bewegt": 0,
  "schnell bewegt": 2,
  "sehr schnell/ausweichend": 4,
  "bewegtes körperteil": 2,
};

const SIGHT = {
  Dunst: 2,
  Nebel: 4,
  Dämmerung: 2,
  Mondlicht: 4,
  Sternenlicht: 6,
  Finsternis: 8,
  Unsichtbar: 8,
};

let Dämmerungssicht = -1;
let Nachsicht = 0.5;
let Nachtblind = 2;

const SIZE = {
  Münze: 8,
  Katze: 6,
  Reh: 4,
  Humanoid: 2,
  Pferd: 0,
  Riese: -2,
  "großer Drache": -4,
};
const COVER = {
  "halbe Deckung/großes Schild": 2,
  "Dreivierteldeckung/sehr großes Schild": 4,
};

const TALENT = {
  Entfernungssinn: -2,
  Einäugig: 4,
  Farbenblind: 4,
};

const MODI = {
  "Steilschuss-unten": 2,
  "Steilschuss-oben": 4,
  "Steilwurf-oben": 8,
  Seitenwind: 4,
  "starker Seitenwind": 8,
};
const HUMANOIDZONE = {
  Kopf: [10, 7, 5],
  Brust: [6, 4, 3],
  Arme: [10, 7, 5],
  Bauch: [6, 4, 3],
  Beine: [8, 5, 4],
  "Hand/Fuß": [16, 11, 8],
  "Auge/Herz": [20, 13, 10],
};
const ANIMALZONE = {
  Kopf: [16, 11, 8],
  Rumpf: [4, 3, 2],
  Bein: [10, 7, 5],
  "verwundbare Stelle": [12, 8, 6],
  Schwanz: [
    [8, 16],
    [5, 11],
    [4, 8],
  ],
  Sinnesorgane: [16, 11, 8],
};

// FK - Deckung - Sicht + herrausragende Sicht(talent) - größe - bewegung -entfernung
</script>
<style lang="scss" scoped></style>
