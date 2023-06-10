<script setup>
import NineBox from './components/NineBox.vue';
const STATUS = {
  Q1_METHOD_ONE: 0,
  Q1_METHOD_TWO: 1,
  Q2_METHOD_ONE: 2,
};
const nineBoxSpec = {
  boxCount: 9,
  ballCount: 4,
  ballSize: 30,
  ballTotalOffset: 500,
  ballPositions: ['left top','right top','left bottom', 'right bottom'],
  column: 3,
  gap: 10,
  status: STATUS.Q2_METHOD_ONE,
  assignPosition: { top: '305px', left: '605px'}
}
</script>

<template>
  <NineBox :spec="nineBoxSpec"/>
</template>

<style lang="scss" scoped>
</style>