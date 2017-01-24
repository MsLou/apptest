<template>
  <div class="info">
    <div v-if="pageIndexed === 1">
      <div class="info__head">
        <h2 class="info__head__title" :class="titleState">vue</h2>
      </div>
      <div class="info__body__portrait">
        <div class="info__body__portrait__pic" :class="picState">
          <img src="./../../assets/img/photo2.jpg" alt="">
        </div>
      </div>
      <div class="info__body" :class="bodyState">
        <p>生活是一种绵延不绝的渴望,渴望不断上升,变得更伟大而高贵。</p>
        <p>vue-router</p>
        <p>vux</p>
        <p>vue-resource</p>
        <p>lxd2017@163.com</p>
      </div>
    </div>
  </div>
</template>
<script>
  // import page1 from './../../components/page1'

  const timesObj = {}

  export default {
    created () {
      this.titleState = 'title__move'
    },
    props: {
      pageIndex: {
        type: Number,
        default: 1
      },
      isPageAnimation: {
        type: Boolean
      }
    },
    data () {
      return {
        titleState: false,
        picState: false,
        bodyState: false,
        pageIndexed: 1
      }
    },
    methods: {
      init () {
        this.titleState = false
        this.picState = false
        this.bodyState = false
        for (let time in timesObj) {
          clearTimeout(time)
        }
        timesObj.initTime = setTimeout(() => {
          this.titleState = 'title__move'
        }, 0)
      }
    },
    watch: {
      titleState (val) {
        if (!val) return
        timesObj.titleTime = setTimeout(() => {
          this.picState = 'pic__scale'
        }, 500)
      },
      picState (val) {
        if (!val) return
        timesObj.picTime = setTimeout(() => {
          this.bodyState = 'body__rotate'
        }, 500)
      },
      isPageAnimation () {
        setTimeout(() => {
          this.pageIndexed = this.pageIndex
        }, 500)
      },
      pageIndexed () {
        this.init()
      }
    }
  }

</script>
<style lang=scss scoped>
  @import "./../../assets/css/mixin.scss";
  .info {
    @include full-screen;
    &__head {
      &__title {
        color: #fff;
        text-align: center;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 2.8rem;
        font-size: .6rem;
        transform: translate3d(0, -3rem, 0);
      }
    }
    &__body {
      transform: translate3d(9rem, 0, 0);
      margin-top: .8rem;
      > p {
        color: #f1e5e5;
        font-size: .25rem;
        line-height: 1.4;
        text-align: center;
        margin-bottom: .2rem;
      }
      &__portrait {
        margin-top: .2rem;
        @include flex-center;
        &__pic {
          border-radius: 50%;
          width: 3rem;
          height: 3rem;
          overflow: hidden;
          transform: scale(0, 0);
        }
      }
    }
  }
  .title__move {
    animation: move .5s forwards;
  }
  @keyframes move {
    0% {
      transform: translate3d(0, -3rem, 0);
    }
    50% {
      transform: translate3d(0, .3rem, 0);
    }
    70% {
      transform: translate3d(0, -.1rem, 0);
    }
    85% {
      transform: translate3d(0, .1rem, 0);
    }
    100% {
      transform: translate3d(0, 0, 0);
    }
  }
  .pic__scale {
    animation:  picScale .5s forwards;
  }
  @keyframes picScale {
    0% {
      transform: scale3d(0, 0, 0);
    }
    100% {
      transform: scale3d(1, 1, 1);
    }
  }
  .body__rotate {
    animation:  bodyRotate .5s forwards;
  }
  @keyframes bodyRotate {
    0% {
      transform: translate3d(9rem, 0, 0);
    }
    100% {
      transform: translate3d(0, 0, 0);
    }
  }
</style>
