<script setup lang="ts">
import { useTemplateRef } from "vue";
import DiscList from "@/components/DiscList.vue";
import Result from "@/components/Result.vue";

let discs = useTemplateRef("discs");
</script>

<template>
    <div class="main">
        <div class="left-view">
            <DiscList ref="discs" class="discs"/>
        </div>
        <!-- @vue-ignore -->
        <Result :score=discs?.allDiscMethod(discs?.DiscMethod.Score) />
    </div>
</template>

<style scoped lang="scss">
.main {
    display: flex;
    flex-grow: 1;
}

.left-view {
    display: flex;
    flex-grow: 1;
    flex-direction: column;
}

.discs {
    margin: 4vw;
}
</style>
