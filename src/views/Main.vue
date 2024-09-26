<script setup>
import Disc from "/src/components/Disc.vue";
</script>

<template>
    <div class="main">
        <div class="discs">
            <div>
                <Disc number="1"/>
                <Disc number="2"/>
                <Disc number="3"/>
            </div>
            <div>
                <Disc number="4"/>
                <Disc number="5"/>
                <Disc number="6"/>
            </div>
        </div>
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
