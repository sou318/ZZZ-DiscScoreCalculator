<script setup lang="ts">
defineProps([
    "score"
]);
</script>

<template>
    <div class="result">
        <div class="score">RESULT SCORE: {{ score }}</div>
        <div class="rank">RANK: {{ score > 100 ? "S" : "?" }}</div>
    </div>
</template>

<style scoped lang="scss">
.result {
    background-color: #222;
    width: 50vw;
    padding: 1vh 0.75vw;
    box-sizing: border-box;
}

.score, .rank {
    font-size: 1.75rem;
}
</style>
