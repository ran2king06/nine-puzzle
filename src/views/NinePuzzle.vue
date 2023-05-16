<template>
  <h2>題目：</h2>
  <div class="main-container first-quiz">
    <div v-for="index in 4" :key="index" class="ball"><div class="num-text">{{ index }}</div></div>
    <div v-for="index in 9" :key="index" class="puzzle-box" :class="[index === 3 || index === 5 || index === 9 ? 'puzzle-blink' : '']"></div>
  </div>
  <p>
    1 & 3 使用 Left 來移動 <br>
    2 & 4 使用 Transform 來移動
  </p>

  <h2>加分項目：</h2>
  <h3>1.四個實心圓可以同時向右下方移動</h3>
  <div class="main-container add-quiz">
    <div v-for="index in 4" :key="index" class="ball" :style="{ left: setBallLeft(index), top: setBallTop(index) }"></div>
    <div v-for="index in 9" :key="index" class="puzzle-box" :class="[index === 3 || index === 5 || index === 9 ? 'puzzle-blink' : '']"></div>
  </div>
  <h3>2.先取決從左至右生成還是上至下，透過倍數去計算left和top的x和y，例:style="{ left: x, top: y}"</h3>
</template>

<script>
import './../assets/animation.css'

export default {
  name: 'NinePuzzle',
  components: {
  },

  setup () {
    const setBallLeft = (index) => {
      if (index % 2 === 0) {
        return 520 + 'px'
      } else {
        return 100 + 'px'
      }
    }

    const setBallTop = (index) => {
      let d = 220 * (index - 3)
      if (d >= 0) {
        if (index % 2 === 0) {
          return 50 + (d) + 'px'
        } else {
          return 50 + (220 * (index - 2)) + 'px'
        }
      } else {
        d = 0
        return 50 + (d) + 'px'
      }
    }

    return {
      setBallLeft,
      setBallTop
    }
  }
}
</script>
<style lang="sass" scoped>

.main-container
  display: grid
  grid-template-columns: 200px 200px 200px
  gap: 10px
  position: relative
  max-width: 620px
  overflow: hidden

.puzzle-box
  width: 200px
  height: 100px
  border: black solid 2px
  box-sizing: border-box
  background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%)

.ball
  position: absolute
  width: 50px
  height: 50px
  background: aqua
  border-radius: 100%
  z-index: 1
  opacity: 100%

// 題目
.first-quiz
  .ball:nth-child(1)
    top: 50px
    transform: translate(-50%, -50%)
    left: 100px
    animation: ball-move 3s infinite ease-in-out

  .ball:nth-child(2)
    transform: translate(495px, -50%)
    top: 50px
    animation: ball-transform 3s infinite ease-in-out

  .ball:nth-child(3)
    top: 270px
    transform: translate(-50%, -50%)
    left: 100px
    animation: ball-move 3s infinite ease-in-out

  .ball:nth-child(4)
    transform: translate(495px, -50%)
    top: 270px
    animation: ball-transform 3s infinite ease-in-out

// 加分
.add-quiz .ball
  transform: translate(-50%, -50%)
  animation: ball-move-corner 3s infinite ease-in-out

.num-text
  position: absolute
  transform: translate(-50%, -50%)
  left: 50%
  top: 50%

// 動態
.puzzle-blink
  animation: fade-in 3s infinite ease-in-out</style>
