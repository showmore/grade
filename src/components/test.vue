<template> 
<div class="windspeed_choose">
      <div class="mode_title">
        选择数值
      </div>
      <div  class="wind_txt">
      <div id="wind_txt_value">{{WindValue}}</div>
      </div>
      <div class="mode_items">
 
        <div class="wind_auto">
          <!-- <img src="../../static/img/auto_mode.png"> -->
        </div>
        <div class="wind_range">
          <mt-range
            v-model="WindValue"
            :min="0"
            :max="100"
            :step="1"
            :bar-height="6"
            @input="inputEvent()"
            @change="changeEvent()"
          >
          </mt-range>
        </div>
 
      </div>
</div>
</template>
<script>
import { Range } from "mint-ui";

export default {
  name: 'ControllPage',
  data(){
   return {
      WindValue:65
   }
},
methods:{
   inputEvent:function(){
      console.log("input事件触发啦，滑竿上的值为-----"+this.WindValue);
   },
   changeEvent:function(){
      console.log("change事件触发啦，滑动停止后的值为-----"+this.WindValue);
   }
},
watch:{
   WindValue(newValue, oldValue){
      let windage_wdth = document.getElementsByClassName('wind_range')[0].clientWidth;    
     //获取到下面滑竿所在div的宽度
      let ave = (windage_wdth-30)/100;  
     //将宽度减去上面显示数字div的宽度后，均分为100份，这里可以改为你自己的范围值，我这里是100，所以除数为100.数字div的宽度为40，但是经过调整后，改为30
      let left_value = parseFloat(72+ave*newValue).toFixed(0) ;  
     //在这里加上了初始偏移量，因为前面还有个图片，可以根据你的布局进行动态调整
 document.getElementById('wind_txt_value').style.transform='translateX('+left_value+'px)';
//调用CSS中的translateX进行动态偏移
 
      }
   }
}


</script>
    <style scoped>
      .mode_items{width:100%;height:calc(100% - 50px);display:flex;overflow-x: hidden;}
      /* .wind_auto{height:100%;width:23px;margin-left: 41px;align-content: center;margin-right:10px;} */
      .wind_auto > img{width:23px;height:23px;}
      .wind_range{height:100%;width:calc(100% - 65px);margin-right:41px;}
      .wind_txt{width:100%;height:auto;text-align: center;font-family: PingFangSC-Regular; font-size: 18px;  color: #666666;margin-bottom: 5px;   }
      #wind_txt_value{width:40px;transform: translateX(72px);}
    </style>
