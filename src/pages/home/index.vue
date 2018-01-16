<template>
  <div class="main">
    <header class="header">
      <div class="back iconfont">&#xe624;</div>
      <div class="search"><a href="#" class="prompt">输入城市/景点/游玩主题</a></div>
      <div class="city">城市</div>
    </header>
    <slider :sliders = sliders></slider>  
  </div>
</template>
<script>
  import axios from 'axios'
  import Slider from './slider'
  export default {
    name: 'Index-main',
    data () {
      return {
        sliders: []
      }
    },
    components: {
      Slider
    },
    methods: {
      getIndexData () {
        axios.get('/api/index.json')
          .then(this.handleDataSuss, this)
          .catch(this.handleDataErr, this)
      },
      handleDataSuss (res) {
        res = res ? res.data : null
        if (res && res.ret && res.data) {
          res.data.slider && (this.sliders = res.data.slider)
          console.log(this.sliders)
        } else {
          this.handleDataError()
        }
      }
    },
    created () {
      this.getIndexData()
    }
  }
</script>
<style scoped lang="stylus">
  .main
    display: flex
    flex-direction: column
    position: absolute
    left: 0
    right: 0
    bottom: 0
    top: 0
    .header 
      display: flex;
      background: #05bad5;
      color: #fff;
      .back
        width: .64rem;
        line-height: .86rem;
        text-align: center;
      .search
        flex: 1;
        margin: .14rem .18rem;
        background: #fff;
        border-radius: .1rem;
      .icon-shuaxin 
        color: #ccc;
        font-size: 0.26rem;
        padding:0 0.15rem;
      .prompt
        font-size: 0.26rem;
        color: #ccc;
        line-height: 0.6rem;
      .city
        width: 1.14rem;
        line-height: .86rem;
        text-align: left;
        .city::after
          content:"";
          display: block;
          width: 0px;
          height: 0px;
          border: 0.1rem solid #fff;
          border-color: white transparent transparent transparent;
          position: absolute;
          right: 0.3rem;
          top: 0.36rem;
</style>