<script setup lang="ts">
import { ref, useTemplateRef } from "vue";
import Disc from "@/components/Disc.vue";
import Result from "@/components/Result.vue";

// init
const disc1 = useTemplateRef("disc1");
const disc2 = useTemplateRef("disc2");
const disc3 = useTemplateRef("disc3");
const disc4 = useTemplateRef("disc4");
const disc5 = useTemplateRef("disc5");
const disc6 = useTemplateRef("disc6");

function getAllDiscScore() {
    // init
    let ds1 = disc1.value?.getDiscScore() ?? 0;
    let ds2 = disc2.value?.getDiscScore() ?? 0;
    let ds3 = disc3.value?.getDiscScore() ?? 0;
    let ds4 = disc4.value?.getDiscScore() ?? 0;
    let ds5 = disc5.value?.getDiscScore() ?? 0;
    let ds6 = disc6.value?.getDiscScore() ?? 0;
    return ds1 + ds2 + ds3 + ds4 + ds5 + ds6;
}
</script>

<template>
    <div class="main">
        <div class="discs">
            <div>
                <Disc ref="disc1" number="1"/>
                <Disc ref="disc2" number="2"/>
                <Disc ref="disc3" number="3"/>
            </div>
            <div>
                <Disc ref="disc4" number="4"/>
                <Disc ref="disc5" number="5"/>
                <Disc ref="disc6" number="6"/>
            </div>
        </div>
        <Result :score=getAllDiscScore() />
    </div>
</template>

<style scoped lang="scss">
    .main {
        display: flex;
        flex-grow: 1;
    }

    .discs {
        flex-grow: 1;
        justify-content: space-evenly;
        align-items: center;

        display: flex;
        gap: 1rem;

        & > div {
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: space-evenly;
        }
    }
</style>
