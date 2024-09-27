<script setup lang="ts">
defineProps(["number"]);
import { ref, type Ref } from "vue";
import StatusButton from "./StatusButton.vue";

// init counter
const ATK       = ref(0);
const CRIT_Rate = ref(0);
const CRIT_DMG  = ref(0);
const AnoPro    = ref(0);

function getDiscCount(value: Ref) {
    value.value = ATK.value + CRIT_Rate.value + CRIT_DMG.value + AnoPro.value;
}
</script>

<template>
    <div class="disc">
        <div class="number">Disc {{ number }}</div>
        <StatusButton @get-disc-count="getDiscCount" v-model="ATK" name="ATK%"/>
        <StatusButton @get-disc-count="getDiscCount" v-model="CRIT_Rate" name="CRIT Rate"/>
        <StatusButton @get-disc-count="getDiscCount" v-model="CRIT_DMG" name="CRIT DMG%"/>
        <StatusButton @get-disc-count="getDiscCount" v-model="AnoPro" name="Anomaly Proficiency"/>
    </div>
</template>

<style scoped>
.number {
    background-color: #333;
    border-bottom: thin solid black;
}
</style>
