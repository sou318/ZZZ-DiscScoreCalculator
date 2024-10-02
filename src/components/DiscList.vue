<script setup lang="ts">
import { useTemplateRef } from "vue";
import Disc from './Disc.vue';

// init
const disc1 = useTemplateRef("disc1");
const disc2 = useTemplateRef("disc2");
const disc3 = useTemplateRef("disc3");
const disc4 = useTemplateRef("disc4");
const disc5 = useTemplateRef("disc5");
const disc6 = useTemplateRef("disc6");
const discs = [disc1, disc2, disc3, disc4, disc5, disc6];



// Disc
enum DiscMethod {
    ATK         = "getATK",
    CritRate    = "getCritRate",
    CritDMG     = "getCritDMG",
    AnoPro      = "getAnoPro",
    Score       = "getDiscScore",
    CountReset  = "countReset",
}
function allDiscMethod(method: DiscMethod) {
    return discs.reduce((sum, disc) => sum + (disc.value?.[method]() ?? 0), 0);
}

defineExpose({
    DiscMethod,
    allDiscMethod,
});
</script>

<template>
    <div class="discRow">
        <div class="discColumn">
            <Disc ref="disc1" number="1"/>
            <Disc ref="disc2" number="2"/>
            <Disc ref="disc3" number="3"/>
        </div>
        <div class="discColumn">
            <Disc ref="disc4" number="4"/>
            <Disc ref="disc5" number="5"/>
            <Disc ref="disc6" number="6"/>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.discRow {
    flex-grow: 1;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

.discColumn {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    height: 100%;
    width: 20vw;
}
</style>
