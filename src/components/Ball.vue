<script setup>
import { computed, onMounted, ref } from 'vue';
const props = defineProps({
    position: Object,
    status: Number,
    assignPosition: Object
});
const y = '500px';
</script>
<template>
    <div class="ball" :style="[props.position]" :class="{moveOffset: props.status === 1, assignPosition: props.status === 2}">
    </div>
</template>
<style lang="scss" scoped>
.ball {
    position: absolute;
    width: 30px;
    height: 30px;
    background-color: #A5F12B;
    border-radius: 30px;
    transition: all linear .2s;
}

.moveOffset {
    animation: translateBall 5s infinite;
}

.assignPosition {
    animation: positionMove 5s infinite;
}


@keyframes translateBall {
    0% {
        transform: translateX(0);
    }

    100% {
        transform: translate(v-bind(y));
    }
}

@keyframes positionMove {

    100% {
        left: v-bind('props.assignPosition.left');
        top: v-bind('props.assignPosition.top');
    }
}
</style>