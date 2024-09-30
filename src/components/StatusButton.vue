<script setup lang="ts">
import { type Ref, ref } from "vue";

defineProps([
    "name", // 名称
    "rate" // 上昇幅
]);
const discCount = defineModel() as Ref<number>;
const count = ref(0);

defineExpose({
    count,
});
function countUp() {
    if (discCount.value < 4) {
        discCount.value++;
        count.value++;
}}

function countDown() {
    if (0 < count.value) {
        discCount.value--;
        count.value--;
}}
</script>

<template>
    <div
    class="statusbutton"
    @click="countUp"
    @auxclick="countDown"
    oncontextmenu="return false;"
    >
        <div class="name">{{ name }}</div>
        <div class="count">+{{ count }}</div>
        <div class="value">{{ count * rate }}</div>
    </div>
</template>

<style scoped lang="scss">
    .statusbutton {
        width: 20vw;
        display: flex;
        justify-content: space-between;

        background-color: #222;
        font-size: 2vh;
        padding: 1vh;
        transition: 100ms;

        &:hover {
            cursor: pointer;
            background-color: #333;
        }
    }

    .name {
        width: 12vw;
    }
    .count, .value {
        text-align: right;
        width: 1vw;
    }
    .count {
        color: orange;
    }
</style>
