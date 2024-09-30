<script setup lang="ts">
defineProps(["number"]);
import { ref, useTemplateRef } from "vue";
import StatusButton from "./StatusButton.vue";

const discCount = ref(0);

const atk       = useTemplateRef("atk");
const critRate  = useTemplateRef("critRate");
const critDmg   = useTemplateRef("critDmg");
const anoPro    = useTemplateRef("anoPro");

function getDiscScore() {
    let result = 0;
    result += atk       .value?.count ?? 0; // 攻撃力
    result += critRate  .value?.count ?? 0; // 会心率
    result += critDmg   .value?.count ?? 0; // 会心ダメージ
    result += anoPro    .value?.count ?? 0; // 異常マスタリー
    return result;
}

defineExpose({
    getDiscScore
});
</script>

<template>
    <div class="disc">
        <div class="number">Disc {{ number }}</div>
        <StatusButton v-model="discCount" ref="atk"      rate="1" name="ATK%"/>
        <StatusButton v-model="discCount" ref="critRate" rate="1" name="CRIT Rate"/>
        <StatusButton v-model="discCount" ref="critDmg"  rate="1" name="CRIT DMG%"/>
        <StatusButton v-model="discCount" ref="anoPro"   rate="9" name="Anomaly Proficiency"/>
    </div>
</template>

<style scoped>
.number {
    background-color: #333;
    padding-left: 2px;
}
</style>
