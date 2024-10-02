<script setup lang="ts">
import { useTemplateRef } from "vue";
import Disc from "@/components/Disc.vue";
import Result from "@/components/Result.vue";

// init
const disc1 = useTemplateRef("disc1");
const disc2 = useTemplateRef("disc2");
const disc3 = useTemplateRef("disc3");
const disc4 = useTemplateRef("disc4");
const disc5 = useTemplateRef("disc5");
const disc6 = useTemplateRef("disc6");
const discs = [disc1, disc2, disc3, disc4, disc5, disc6];



// ---- Get Methods ---- //
enum DiscMethod {
    ATK         = "getATK",
    CritRate    = "getCritRate",
    CritDMG     = "getCritDMG",
    AnoPro      = "getAnoPro",
    Score       = "getDiscScore",
}
function getAllStatus(method: DiscMethod) {
    return discs.reduce((sum, disc) => sum + (disc.value?.[method]() ?? 0), 0);
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
        <Result :score=getAllStatus(DiscMethod.Score) />
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
