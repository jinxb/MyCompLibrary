<template>
  <div class="progress-ver">
    <div class="progress-bar">
      <!-- 竖向默认外显百分比，支持自定义文字 -->
      <span class="inside-top" :style="`color:${textInsideColor};`">{{ textInsideTop }}</span><span class="inside-top-suffix">{{ topSuffix }}</span>
      <div class="progress-outer" :style="{width:strokeWidth + 'px'}">
        <div class="progress-inner" :style="innerStyle"></div>
      </div>
      <span class="inside-btm">{{ textInsideBtm }}</span><span class="inside-btm-suffix">{{ btmSuffix }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    percentage: {
      // 进度条百分比
      type: Number,
      default: 0,
      required: true,
      valiator(value) {
        return value >= 0 && value <= 100
      }
    },
    strokeWidth: {
      // 进度条粗细，单位px
      type: Number,
      default: 8
    },
    // pType: {
    //   // 进度条 横竖
    //   type: String,
    //   default: 'vertical',
    //   validator: val => ['across', 'vertical'].includes(val)
    // },
    pColor: {
      // 进度条颜色
      type: String,
      default: ''
    },
    textInsideTop: {
      // 横向->前 纵向->上
      type: null,
      default: ''// 默认展示百分比
    },
    textInsideBtm: {
      // 横向->后 纵向->下
      type: null,
      default: '123'// 默认展示百分比
    },
    topSuffix: {
      // top后缀
      type: String,
      default: ''
    },
    btmSuffix: {
      // btm后缀
      type: String,
      default: ''
    },
    textInsideColor: {
      // 文字颜色
      type: String,
      default: ''
    }
  },
  computed: {
    // 竖向height
    innerStyle() {
    // 计算属性调用其他计算属性，必须加this关键字，否则找不到
      console.log(this.textInsideColor)
      return { height: 150 * (parseInt(this.percentage) / 100) + 'px', backgroundColor: this.pColor }
    }
  },
  watch: {
    // percentage(n) {
    //   this.textInsideBtm = n
    // }
  }
}
</script>

<style scoped>
/* 横向 */
/* .progress-hor { */
  /* margin: 10px;
  margin: 0 auto; */
/* } */
/* 竖向 */
.progress-ver {
  margin: 0 auto;
  /* display: flex; */
  flex: 1;
}
/* 进度条的样式 */
.progress-bar {
  margin: 0 auto;
  /* flex: 1; */
  text-align: center;
}
.progress-outer {
    position:relative;
    margin: 5px auto;
    height:150px;
    background-color:#e5e5e5;
}
.progress-inner {
    position:absolute;
    bottom:0px;
    width:100%;
    background-color:#fc5c28;
}
</style>
