<script setup lang="ts">
import { type Ref, ref } from "vue";

const props = defineProps([
    "name", // 名称
    "rate" // 上昇幅
]);
const discCount = defineModel() as Ref<number>;
const count = ref(0);

function getValue() {
    // parseFloatで少数がない場合、整数で返す
    return parseFloat((count.value * props.rate).toFixed(1));
}

function countReset() {
    discCount.value -= count.value - 1;
    count.value = 0;
}

defineExpose({
    count,
    getValue,
    countReset,
});



// ---- カウント ---- //
function countUp() {
    if (
        discCount.value < 5 // 初期サブステが4つある場合5回強化できる
        || count.value == 0 // discCountが4でもステータスが有効化できるように
    ) {
        count.value++;
        // ステータス有効化時、discCountも上がらないように
        if (count.value > 1) {
            discCount.value++;
        }
    }
}

function countDown() {
    if (0 < count.value) {
        count.value--;
        // ステータス無効化時、discCountが下がらないように
        if (count.value > 0) {
            discCount.value--;
        }
    }
}
</script>

<template>
    <div
    class="status"
    @click.middle="countReset"
    @click="countUp"
    @auxclick="countDown"
    >
        <div class="name">{{ name }}</div>
        <div class="count">{{ count == 0 ? "-" : `+${count-1}` }}</div>
        <div class="value">{{ getValue() }}</div>
    </div>
</template>

<style scoped lang="scss">
    .status {
        display: flex;
        justify-content: space-between;

        background-color: #222;
        font-size: 1.2rem;
        padding: 1vh;
        transition: 100ms;

        &:hover {
            cursor: pointer;
            background-color: #333;
        }

        &:active {
            background-color: #2b2b2b;
        }
    }

    .name {
        width: 75%;
    }
    .count, .value {
        text-align: right;
        width: 25%;
    }
    .count {
        color: orange;
    }
</style>
