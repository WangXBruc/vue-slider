<template>
  <div id="Slider">
    <div class="slider-container" @mouseover="stopAnimate" @mouseleave="doTheAnimate">
      <img class="slider-cell" src="/static/images/1.jpg" alt="1" title="1">
      <img class="slider-cell" src="/static/images/2.jpg" alt="2" title="2">
      <img class="slider-cell" src="/static/images/3.jpg" alt="3" title="3">
      <img class="slider-cell" src="/static/images/4.jpg" alt="4" title="4">
      <!--复制一份轮播图-->
      <img class="slider-cell" src="/static/images/1.jpg" alt="1" title="5">
      <img class="slider-cell" src="/static/images/2.jpg" alt="2" title="6">
      <img class="slider-cell" src="/static/images/3.jpg" alt="3" title="7">
      <img class="slider-cell" src="/static/images/4.jpg" alt="4" title="8">
    </div> <!--slider-container-->
  </div>
</template>

<script>
export default {
  name: 'Get',
  data () {
    return{
      companies:["MS-1","Apple-2","Ali-3","Baidu-4","Tencent-5"]
    }
  },
  computed: {
    // .slider-container的jquery实例
    $sliderContainer(){
      return $('.slider-container');
    },
    /**
     * @method
     * @return {string} .sliderWidth 的宽度，以px为单位
     */
    sliderWidth(){
      return $('#Slider').css('width');
    }
  },
  methods: {
    /**
     * @method
     * @description 执行动画
     */
    doTheAnimate(){
      this.$sliderContainer.animate(
        { left: `-${this.sliderWidth}` },
        this.calcTime(),
        'linear',
        // 动画回调函数
        () => {
          this.$sliderContainer.css('left','0');
          if(parseInt(this.$sliderContainer.css('left')) <= 0){
            this.doTheAnimate();
          }
      });
    },
    /**
     * @method
     * @description 鼠标悬停到.slider-container的时候停止动画
     */
    stopAnimate(){
      this.$sliderContainer.stop();
    },
    /**
     * @method
     * @param {number} speed 动画移动的速度
     * @param {number} distance .slider-container距离一半移出#Slider还差多少
     * @return {number} .slider-container距离一半移出#Slider还需要多少时间
     *  从而鼠标移出时，再次执行doTheAnimate时的动画时间会发生变化，以保证动画速度不变
     */
    calcTime(){
      let speed = parseInt(this.sliderWidth)/6000;
      let distance = parseInt(this.sliderWidth) + parseInt(this.$sliderContainer.css('left'));
      return distance/speed;
    }
  },
  mounted () {
    this.doTheAnimate();
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
}
#Slider{
  position: relative;
  width:100%;
  /*移处元素之间空格导致的间隙*/
  font-size: 0;
  height: 100px;
  overflow: hidden;
}
.slider-container{
  position: absolute;
  top: 0;
  left: 0;
  width: 200%;
  height: 100%;
}
img.slider-cell{
  width: 12%;
  margin-right: .5%;
  height: 100px;
}
img.slider-cell:hover{
  cursor: pointer;
}
</style>


