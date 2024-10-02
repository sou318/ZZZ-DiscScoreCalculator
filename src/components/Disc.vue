<script setup lang="ts">
defineProps(["number"]);
import { ref, useTemplateRef } from "vue";
import Status from "./Status.vue";

const discCount = ref(0);

// 増加幅
const Rate_ATK         = 3;
const Rate_CritRate    = 2.4;
const Rate_CritDMG     = 4.8;
const Rate_AnoPro      = 9;

// 子要素を使用
const Ref_ATK       = useTemplateRef("ATK");
const Ref_CritRate  = useTemplateRef("CritRate");
const Ref_CritDMG   = useTemplateRef("CritDMG");
const Ref_AnoPro    = useTemplateRef("AnoPro");



// --- Score and Rank --- //
function getATK     () { return Ref_ATK     .value?.getValue() ?? 0; }
function getCritRate() { return Ref_CritRate.value?.getValue() ?? 0; }
function getCritDMG () { return Ref_CritDMG .value?.getValue() ?? 0; }
function getAnoPro  () { return Ref_AnoPro  .value?.getValue() ?? 0; }

function getDiscScore() {
    let result = 0;

    // init
    let ATK         = Ref_ATK       .value?.count ?? 0; // 攻撃力
    let CritRate    = Ref_CritRate  .value?.count ?? 0; // 会心率
    let CritDMG     = Ref_CritDMG   .value?.count ?? 0; // 会心ダメージ
    let AnoPro      = Ref_AnoPro    .value?.count ?? 0; // 異常マスタリー
    result += ATK       * 12;
    result += CritRate  * 14;
    result += CritDMG   * 13;
    result += AnoPro    * 11;
    return parseFloat(result.toFixed(2));
}

function getDiscRank(score: number) {
    if (score >= 110) return "SSS";
    if (score >= 100) return "SS";
    if (score >=  90) return "S";
    if (score >=  80) return "A";
    if (score >=  50) return "B";
    return "X";
}



// --- other --- //
function countReset() {
    Ref_ATK     .value?.countReset();
    Ref_CritRate.value?.countReset();
    Ref_CritDMG .value?.countReset();
    Ref_AnoPro  .value?.countReset();
    discCount.value = 0;
}

defineExpose({
    getATK,
    getCritRate,
    getCritDMG,
    getAnoPro,
    getDiscScore,
    countReset,
});
</script>

<template>
    <div class="disc">
        <div class="title">
            <div class="number" @click="countReset">Disc {{ number }}</div>
            <div class="score">SCORE: {{ getDiscScore() }}</div>
            <div class="rank">{{ getDiscRank(getDiscScore()) }}</div>
        </div>
        <Status v-model="discCount" ref="ATK"      :rate=Rate_ATK        name="ATK%"/>
        <Status v-model="discCount" ref="CritRate" :rate=Rate_CritRate   name="CRIT Rate"/>
        <Status v-model="discCount" ref="CritDMG"  :rate=Rate_CritDMG    name="CRIT DMG%"/>
        <Status v-model="discCount" ref="AnoPro"   :rate=Rate_AnoPro     name="Anomaly Proficiency"/>
    </div>
</template>

<style scoped lang="scss">
.title {
    min-width: 20vw;
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    font-size: 1rem;
    background-color: #333;
}

.number {
    transition: 100ms;
    padding-left: 2px;

    &:hover {
        color: transparent;
        cursor: pointer;

        &::before {
            color: red;
        }
    }

    &::before {
        color: transparent;
        position: absolute;
        transition: 100ms;
        content: "RESET";
    }
}

.score {
    margin-left: auto;
    width: 6rem;
    margin-right: 0.5vw;
}

.rank {
    padding-right: 5px;
    text-align: right;
    width: 10%;
}
</style>
