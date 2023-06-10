<script setup>
const props = defineProps({
    column: Number,
    gap: Number,
    shineToggle: Boolean,
    isLastRow: Boolean,
    isLastColumn: Boolean
});
</script>
<template>
    <div class="rect" :class="{ shineAni: shineToggle, isLastRow: isLastRow, isLastColumn: isLastColumn }">      
    </div>
</template>
<style lang="scss" scoped>
.rect {
    width: 200px;
    height: 100px;
    border: black solid 2px;
    background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%);
    margin-bottom: calc(v-bind('gap') * 1px );
    margin-right: calc(v-bind('gap') * 1px );
}

.isLastRow {
    margin-bottom: 0;
}

.isLastColumn {
    margin-right: 0;
}
.shineAni {
    animation: shineAni 1.5s  ease-in-out infinite;
}

@keyframes shineAni {
    0% {
        opacity: 1;
    }

    60% {
        opacity: 0.6;
    }

    100% {
        opacity: 1;
    }
}
</style>