# Neutec 前端面試題目
## Description

製作 **NineBox.vue** 方便不同頁面引入使用
在 **NineBox** 拆出 **Rect** 方格元件與 **Ball** 球體元件方便各別控制與新增球體
並能根據不同情境創造九宮格外的不同組合
透由 **NineBox** 當做 **Controller** 統一對單元控制統一更新球體位置
球體只需要拿到新的位置負責更新
球體移動分別使用兩種常見方法 **css animation** 與 **js requestAnimationFrame**
雖然 gsap 宣稱已經能做到 **js requestAnimationFrame** 與 **css animation** 效能不分軒輊
但如果非複雜操作還是會以選擇 **css  animation** 實作，因此進階題使用之。


## Tech Stack

Vue `^3.3.2`
Vite `^4.3.5`

## Getting Started


```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Use Example

**component.vue**
```
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

<template>
  <NineBox :spec="nineBoxSpec"/>
</template>
```
### Component props

The majority of settings for the component are configured using props:


| Name | Type  | Description |
| -------- | --------  | --------|
| boxCount     | Number     | 格子數量  |
| ballCount     | Number     | 球體數量  |
| ballSize     | Number     | 球體大小  |
| ballTotalOffset     | Number     | 題目一動畫移動量  |
| ballPositions     | Array     | 四顆球各自位置  |
| column    | Number     | 列數  |
| gap    | Number     | 格子間的間隔大小  |
| status    | Number     | 0 基本題解法一 / 1 基本題解法二 / 2 進階題  |
| assignPosition    | Object     | 進階題移動位置  |


