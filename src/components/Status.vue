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

defineExpose({
    count,
    getValue
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
    @click="countUp"
    @auxclick="countDown"
    oncontextmenu="return false;"
    >
        <div class="name">{{ name }}</div>
        <div class="count">{{ count == 0 ? "-" : `+${count-1}` }}</div>
        <div class="value">{{ getValue() }}</div>
    </div>
</template>

<style scoped lang="scss">
    .status {
        width: 20vw;
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
        width: 12vw;
    }
    .count, .value {
        text-align: right;
        width: 2vw;
    }
    .count {
        color: orange;
    }
</style>
