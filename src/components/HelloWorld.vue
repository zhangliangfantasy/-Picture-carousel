<template>
  <div id="app">
    <div class="container">
      <div v-for="(item, index) in List" class="images" :key="index">
        <img class="imge"  :style="{'border': styleObject[item] ? '2px solid red': '', 'opacity': styleObject[item] ? '1': ''}" :src="cats(item)" @click="active(item)" />
        <div class="title">{{item}}</div>
      </div>
      <div class="blank">
        <div class="blank-child"></div>
        <div class="blank-title">h</div>
      </div>
       <div class="blank">
        <div class="blank-child"></div>
        <div class="blank-title">i</div>
      </div>
    </div>
    <div class="point">
      >>>
    </div>
    <div class="info" v-for="(item, index) in List" :key="index" v-if="isShow[item]">
      <img class="img" :src="cats(item)" width="300px" height="300px"/>
    </div>
   <!-- <div class="info" v-else>
    </div>  -->
  </div>
</template>

<script>
// import FadeAnimation from '../common/FadeAnimation'
export default {
  data () {
    return {
      cat: 'static/cat/cat_a.jpg',
      List: ['a', 'b', 'c', 'd', 'e', 'f', 'g'],
      isShow: {},
      isActive: {},
      styleObject: {},
      cycle: undefined
    }
  },
  // components: {
  //   FadeAnimation
  // },
  methods: {
    cats (item) {
      return 'static/cat/cat_' + item + '.jpg'
    },
    active (item) {
      for (let item of this.List) {
        this.$set(this.isShow, item, false)
      }
      if (!this.isShow[item]) {
        this.isShow[item] = true
      }
    },
    init () {
      for (let item of this.List) {
        this.$set(this.styleObject, item, false)
      }
      let index = 0
      let that = this
      if (this.cycle) {
        clearInterval(this.cycle)
      }
      this.cycle = setInterval(function () {
        for (let item of that.List) {
          that.styleObject[item] = false
          that.$set(that.isShow, item, false)
        }
        let item = that.List[index]
        if (!that.isShow[item]) {
          that.isShow[item] = true
        }
        that.styleObject[item] = true
        index = (index + 1) % that.List.length
      }, 3000)
    }
  },
  mounted () {
    this.init()
  }
}
</script>

<style scoped>
  #app {
    display: flex;
    align-items: center;
  }
  .container {
    width: 420px;
    height: 450px;
    background: #ccc;
    text-align: center;
    margin: 20px;
    overflow: hidden;
  }
  .images {
    float: left;
    margin: 10px 13px;
  }
  .container .imge{
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 2px solid rgb(73, 54, 54);
    opacity: 0.5;
    transition: all .2s ease-in-out;
  }
  .images:hover .imge{
    cursor: pointer;
    transform: scale(1.2);
    border: 2px solid red;
    opacity:1;
  }
  .container .title {
    height: 26px;
    line-height: 26px;
  }
  .blank {
    float: left;
    margin: 10px 13px;
  }
  .blank-child {
    width: 100px;
    height:100px;
    background-color:rgb(252, 248, 248);
    border-radius: 50%;
     border: 2px solid rgb(73, 54, 54);
  }
  .blank-title {
    height: 26px;
    line-height: 26px;
  }
  .point {
    width: 100px;
    text-align: center;
    font-size: 30px;
    font-weight: bold;
    animation: simple 1s linear infinite;
  }
  @keyframes simple {
    50% {
      transform: translateX(10px);
      opacity: 1;
    }
    100% {
      tranform: translateX(10px);
      opacity: 0;
    }
  }
  .info {
    margin: 20px;
    width: 300px;
    height: 300px;
    background-color: pink;
    opacity: 0;
    animation: simple1 3s linear 1;
  }
   @keyframes simple1 {
    50% {
      transform: translateX(10px);
      opacity: 1;
    }
    100% {
      tranform: translateX(10px);
      opacity: 0;
    }
  }
</style>
