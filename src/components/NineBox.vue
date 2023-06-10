<script setup>

// 引入元件
import Rect from './Rectangle.vue';
import Ball from './Ball.vue';
import { ref, onMounted } from 'vue';

// 接收元件參數
const props = defineProps({
    spec: Object
});

// 計算該方格是否為最後一行
function lastRow(idx) {
    const rowNum = Math.trunc((idx - 1 ) / props.spec.column);
    return rowNum == Math.ceil( props.spec.boxCount / props.spec.column ) - 1;
}

// 計算該方格是否為最後一列
function lastColumn(idx) {
    const columnNum = idx % props.spec.column;
    return columnNum === 0;
} 

// 偶數列且為該列最後一格與基數列且為該列倒數第二格需閃爍
function shineDetect(idx) {
    const columnNum = idx % props.spec.column;
    const rowNum = Math.trunc((idx - 1 ) / props.spec.column);
    return (columnNum === 0 && rowNum % 2 === 0) || (columnNum === props.spec.column - 1 && rowNum % 2 !== 0);
}

// 球體橫移移動變量
const offset = ref(0);
function animation() {
    offset.value += 1;
    // 移動 500px 後停止
    if (offset.value <= props.spec.ballTotalOffset) {
        requestAnimationFrame(animation);
    }
};

// 幫所有球體計算位置並控制每顆球
function positionConvert(position) {
    const totalRow = Math.ceil( props.spec.boxCount / props.spec.column );
    const totalWidth = props.spec.column * 200 + props.spec.gap * (props.spec.column - 1);
    const totalHeight = totalRow * 100 + props.spec.gap * (totalRow - 1);
    const horizontal = position.split(' ')[0];
    const vertical = position.split(' ')[1];
    let style = {};
    const ballHalf = props.spec.ballSize / 2;

    // 根據 ballPosition 決定該球於九宮格四角的位置
    switch (horizontal) {
        case 'left':
            style.left = `${ 100 - ballHalf }px`;
            break;
        case 'right':
            style.left = `${totalWidth - 100 - ballHalf}px`;
        default:
            break;
    }
    switch (vertical) {
        case 'top':
            style.top = `${ 50 - ballHalf}px`;
            break;
        case 'bottom':
            style.top = `${totalHeight - 50 - ballHalf}px`;
    }
    // 根據 offset 使球體 left 增加達到橫移
    style.left = `${parseInt(style.left.split('px')[0]) + offset.value % 500}px`;
    return style;
};
onMounted(()=>{
    if(props.spec.status === 0)
        requestAnimationFrame(animation);
});
</script>
<template>
    <div class="box-container">
        <Rect v-for="index in spec.boxCount" :key="index" :column="spec.column" :gap="spec.gap" :shineToggle="shineDetect(index)" :isLastRow="lastRow(index)" :isLastColumn="lastColumn(index)"/>
        <Ball v-for="index in spec.ballCount" :key="index" :position="positionConvert(spec.ballPositions[index - 1])" :status="spec.status" :assignPosition="spec.assignPosition" :totalOffset="props.spec.ballTotalOffset"/>
   </div>
</template>
<style lang="scss" scoped>
.box-container {
    position: relative;
    display: flex;
    flex-wrap: wrap;
    overflow: hidden;
    background: #fff;
    // 計算九宮格外圍
    width: calc(v-bind('spec.column') * 200px + (v-bind( 'spec.column' ) - 1) * v-bind('spec.gap') * 1px);
}
</style>