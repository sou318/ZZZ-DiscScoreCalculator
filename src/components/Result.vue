<script setup lang="ts">
defineProps([
    "score"
]);

function getRank(score: number) {
    if (score >= 700) return "EX";
    if (score >= 600) return "SSS";
    if (score >= 500) return "SS";
    if (score >= 400) return "S";
    if (score >= 300) return "A";
    if (score >= 200) return "B";
    return "X";
}
</script>

<template>
    <div class="result">
        <div class="main-result">
            <div class="score">SCORE: {{ score }}</div>
            <div class="rank">{{ getRank(score) }}</div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.result {
    background-color: #222;
    width: 50vw;
    padding: 1vh 0.75vw;
    box-sizing: border-box;
}

.main-result {
    font-size: 4vw;
    line-height: 100%;
    margin-top: -1vh;

    display: flex;
    justify-content: space-evenly;

    border-bottom: thin solid white;

    .score, .rank {
        width: 50%;
    }

    .rank {
        text-align: center;
    }
}
</style>
