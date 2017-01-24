<template>
  <div class="app">
    <page2 ref="page2" :pageIndex="pageIndex" :isPageAnimation="isPageAnimation" :style="{ transition: page2.transition, transform: `translate3d(0, ${page2.translateY}, 0)` }"></page2>
    <page1 ref="page1" :pageIndex="pageIndex" :isPageAnimation="isPageAnimation" :style="{ transition: page1.transition, transform: `translate3d(0, ${page1.translateY}, 0)` }"></page1>
    <next :pageMoveing="pageMoveing" :setIndex="setIndex" :setPageAnimation="setPageAnimation" :pages="pages"></next>
  </div>
</template>
<script>
  import page1 from './../basicinfo'
  import page2 from './../aboutme'
  import next from './next'

  export default {
    created () {
      document.querySelector('body').addEventListener('touchstart', (ev) => {
        ev.preventDefault()
      })
    },
    mounted () {
      this.pages = this.getPageEl()
    },
    data () {
      return {
        page1: {
          translateY: '0px',
          transition: '0s'
        },
        page2: {
          translateY: '0px',
          transition: '0s'
        },
        pageIndex: 1,
        pages: [],
        isPageAnimation: true // 动画是否结束
      }
    },
    methods: {
      pageMoveing (num, index, isTrans) {
        if (isTrans) {
          this[`page${index}`].transition = '.5s'
        } else {
          this[`page${index}`].transition = '0s'
        }
        this[`page${index}`].translateY = `${num}px`
      },
      setIndex (index) {
        this.pageIndex = index
      },
      setPageAnimation (isOk) {
        this.isPageAnimation = isOk
      },
      getPageEl () {
        const pages = []
        for (let i = 1; i < 10; i += 1) {
          const page = this.$refs[`page${i}`]
          if (page) {
            pages.push(page)
          }
        }
        return pages
      }
    },
    components: {
      next,
      page1,
      page2
    }
  }

</script>
<style lang=scss scoped>
  .app {
    height: 100%;
  }
</style>
