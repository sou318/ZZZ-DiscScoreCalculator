<script setup lang="ts">
defineProps(["number"]);
import { ref } from "vue";
import StatusButton from "./StatusButton.vue";

const discEnhanceCount = ref(0);
</script>

<template>
    <div class="disc">
        <div class="number">Disc {{ number }}</div>
        <StatusButton v-model="discEnhanceCount" name="ATK%"/>
        <StatusButton v-model="discEnhanceCount" name="CRIT Rate"/>
        <StatusButton v-model="discEnhanceCount" name="CRIT DMG%"/>
        <StatusButton v-model="discEnhanceCount" name="Anomaly Proficiency"/>
    </div>
</template>

<style scoped>
.number {
    background-color: #333;
    border-bottom: thin solid black;
}
</style>
