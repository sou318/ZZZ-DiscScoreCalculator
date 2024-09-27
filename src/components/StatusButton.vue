<script setup lang="ts">
defineProps(["name"]);
const emit = defineEmits(["getDiscCount"]);
const count: Ref = defineModel();

import { type Ref, ref } from "vue";

function countUp() {
    // get the total disc enhance count
    const nowCount = ref(0);
    emit("getDiscCount", nowCount);

    if (nowCount.value < 4) {
        count.value++;
}}

function countDown() {
    if (0 < count.value) {
        count.value--;
}}
</script>

<template>
    <div class="statusbutton">
        <div class="name">{{ name }}</div>
        <div class="button" @click="countDown">-</div>
        <div>{{ count }}</div>
        <div class="button" @click="countUp">+</div>
    </div>
</template>

<style scoped lang="scss">
    .statusbutton {
        display: flex;
        background-color: #222;
        font-size: 2vh;

        & * {
            padding: 1vh;

            display: flex;
            flex-direction: column;
            justify-content: center;
            align-content: center;
        }
    }

    .name {
        width: 10vw;
    }

    .button {
        user-select: none;
        text-align: center;
        width: 1vw;
        aspect-ratio: 1;

        &:hover {
            cursor: pointer;
            background-color: #fff1;
        }
    }
</style>
