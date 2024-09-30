<script setup lang="ts">
defineProps(["number"]);
import { ref, useTemplateRef } from "vue";
import StatusButton from "./StatusButton.vue";

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

/**
 * このディスク単体のスコアを取得する物です。
 * ディスク全て合わせて計算する場合、使用しないでください。
 */
function getDiscScore() {
    let result = 0;

    // init
    let ATK         = Ref_ATK       .value?.getValue() ?? 0; // 攻撃力
    let CritRate    = Ref_CritRate  .value?.getValue() ?? 0; // 会心率
    let CritDMG     = Ref_CritDMG   .value?.getValue() ?? 0; // 会心ダメージ
    let AnoPro      = Ref_AnoPro    .value?.getValue() ?? 0; // 異常マスタリー
    // 基礎値
    CritRate += 5;
    CritDMG  += 50;

    // ATK
    result += ATK;

    // CritDmg
    result += CritDMG * (CritRate / 100) - 2.5;

    // AnoPro
    result += AnoPro;

    return parseFloat(result.toFixed(2));
}

defineExpose({
    getDiscScore
});
</script>

<template>
    <div class="disc">
        <div class="number">
            <div>Disc {{ number }}</div>
            <div class="score">SCORE: {{ getDiscScore() }}</div>
        </div>
        <StatusButton v-model="discCount" ref="ATK"      :rate=Rate_ATK        name="ATK%"/>
        <StatusButton v-model="discCount" ref="CritRate" :rate=Rate_CritRate   name="CRIT Rate"/>
        <StatusButton v-model="discCount" ref="CritDMG"  :rate=Rate_CritDMG    name="CRIT DMG%"/>
        <StatusButton v-model="discCount" ref="AnoPro"   :rate=Rate_AnoPro     name="Anomaly Proficiency"/>
    </div>
</template>

<style scoped lang="scss">
.number {
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    background-color: #333;
    padding-left: 2px;

    .score {
        width: 8vw;
    }
}
</style>
