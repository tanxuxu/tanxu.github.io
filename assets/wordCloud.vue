<style media="screen" scoped lang="less">
  .wordCloud{
    margin: 0 auto;
    background: #fcfcfc !important;
  }
  .wordCloud>div{
    margin: 0 auto;
  }
</style>
<template>
    <div :id="wordCloudId" class="wordCloud" v-bind:style="{'width':width+'px','height':height+'px'}">
          <p  v-if="data.length==0" style="text-align:center; position:relative; top: -50%;">无标签</p>
    </div>
</template>
<script>
  import echarts from "echarts";
  //导入标签云扩展
  import wordCloud from 'echarts-wordcloud';
   export default{
     props: {
       width: {
         type: Number,
         default: 500
       },
       height:{
         type: Number,
         default: 105
       },
       gridSize: {
         type: Number,
         default: 10
       },
       data: {
         type: Array,
         default: function(){
           return []
         }
       }
     },
     watch: {
       width: function(val){
         this.resizeWordCloud();   //如果高度有变化，刷新
       },
       data: function(val){
          this.init();
          this.resizeWordCloud();
       }
     },
     data(){
       return {
         chart :null,
         wordCloudId: ""
      }
     },
     created(){
        console.log(this.data);
     },
     mounted(){
        this.init();
     },
     methods:{
       init: function(){
         let _this = this;
         console.log(this.data);
         this.wordCloudId = this.generateMixed();  //生成自动id
         this.$nextTick(function(){
           _this.showWordCloud(_this.wordCloudId,_this.data);
           //点击事件
           _this.chart.on('click',function(params){
              let name = params.name;  //tag
              _this.$emit('click',name);
           });

         });
       },
       generateMixed:function() {
        var chars = ['0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'];
        var n = 5;
        var res = "";
        for(var i = 0; i < n ; i ++) {
          var id = Math.ceil(Math.random()*35);
          res += chars[id];
        }
        return res;
      },
       showWordCloud: function(wordCloudId,res){
         let _this = this;
         let id = wordCloudId+"";
         var dom = document.getElementById(id);
         this.chart = echarts.init(document.getElementById(id));
         var option = {
                series: [ {
                    type: 'wordCloud',
                    gridSize: _this.gridSize,  //文字间距
                    sizeRange: [12,18],  //文字大小范围
                    rotationRange: [0, 0],   //旋转角度
                    shape: 'ellipse',   //椭圆
                    width: _this.width,
                    height: _this.height,
                    drawOutOfBound: false,
                    textStyle: {
                        normal: {
                            color: "#ccc"
                        },
                        emphasis: {
                            color:'#039'
                        }
                    },
                    data: res
                } ]
            };
            debugger;
            this.chart.setOption(option);
            //chart.resize;
       },
       //刷新wordcloud
       resizeWordCloud:function(){
         try {
           this.chart.resize();
         } catch (e) {

         }
       }
     }
   }
</script>
