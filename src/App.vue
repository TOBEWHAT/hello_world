<template>
  <div id="app">
    <div class="typebox">
      <div class="world">{{ obj.output }}</div>
      <span class="typed-cursor">|</span>
    </div>
  </div>
</template>

<script>
import EasyTyper from 'easy-typer-js'
export default {
  name: 'home',
  data() {
    return {
      obj: {
        output: '',
        type: 'normal',
        isEnd: false,
        speed: 90,
        backSpeed: 40,
        sleep: 3000,
        singleBack: false,
        sentencePause: false,
      },
    }
  },
  mounted() {
    // eslint-disable-next-line no-unused-vars
    // const typed = new EasyTyper(this.obj, `Hello Worl`)
    // console.log(typed)
    this.init()
  },
  methods: {
    // 初始化
    init() {
      this.fetchData()
    },
    fetchData() {
      // 一言Api进行打字机循环输出效果
      fetch('https://v1.hitokoto.cn')
        .then((res) => {
          return res.json()
        })
        .then(({ hitokoto }) => {
          this.initTyped(hitokoto)
        })
        .catch((err) => {
          console.error(err)
        })
    },
    initTyped(input, fn, hooks) {
      const obj = this.obj

      // eslint-disable-next-line no-unused-vars
      const typed = new EasyTyper(obj, 'Hello Worl', fn, hooks)
    },
  },
}
</script>

<style lang="stylus">
body
  margin:0px
  padding:0px
.world
  margin:0px
  padding:0px
  float:left
  font-size:120px
  font-font-weight:blod
.typebox
  position:fixed
  left:50%
  top:50%
  transform:translate(-50%,-50%)
  -webkit-transform:translate(-50%,-50%)
  line-height:158px
.typed-cursor
  margin-left: 12px
  margin-top:-12px
  display:block
  float:left
  font-size:98px
  opacity: 1
  -webkit-animation: blink 0.9s infinite
  -moz-animation: blink 0.9s infinite
  animation: blink 0.9s infinite
@keyframes blink
  0%
    opacity: 1
  50%
    opacity: 0
  100%
    opacity: 1

@-webkit-keyframes blink
  0%
    opacity: 1
  50%
    opacity: 0
  100%
    opacity: 1

@-moz-keyframes blink
  0%
    opacity: 1
  50%
    opacity: 0
  100%
    opacity: 1
</style>
