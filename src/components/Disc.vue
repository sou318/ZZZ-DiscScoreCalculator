<script setup>
defineProps(["number"]);
import StatusButton from "./StatusButton.vue";
</script>

<template>
    <div class="disc">
        <div class="number">Disc {{ number }}</div>
        <StatusButton name="ATK%"/>
        <StatusButton name="CRIT Rate"/>
        <StatusButton name="CRIT DMG%"/>
        <StatusButton name="Anomaly Proficiency"/>
    </div>
</template>

<style scoped>
.number {
    background-color: #333;
    border-bottom: thin solid black;
}
</style>
