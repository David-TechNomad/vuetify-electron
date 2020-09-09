<template>
  <!--为echarts准备一个具备大小的容器dom-->
  <div class="echartsView" :style="echartsStyle">
        <h2>{{echartsTitle}}详情</h2>
        <!-- <el-button class="defaultBtn rt mt10" @click="back">返回</el-button> -->
        <!-- <div style="width: 600px;height: 400px;padding:10px;float:left;">
            <h4>饼图</h4>
            <div id="main" style="width: 100%;height: 100%;"></div>
        </div>
        <div style="width: 600px;height: 400px;padding:10px;float:left;">
            <h4>柱状图</h4>
            <div id="main2" style="width: 100%;height: 100%;"></div>
        </div> -->
        <div class="mt20">
            <div class="boxshow echartsItem">
                <h2>饼图</h2>
                <div id="main" class="echartsBox"></div>
            </div>
            <!-- <div class="boxshow echartsItem">
                <h2>柱状图</h2>
                <div id="main2" class="echartsBox"></div>
            </div> -->
            <div class="clear"></div>
        </div>
  </div>
</template>

<script>
  import echarts from 'echarts'
  export default {
      name: '',
      data () {
          return {
              code:'',
              echartsTitle:'',
              charts: '',
              echartsStyle: {
                "height": Number(document.documentElement.clientHeight)+'px',
                "width":'100%',
                "background":"#ffffff"
            },
              seriesData:[],
              xAxisData:[],
              type:'',
              opinion:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎'],
              opinionData:[
                {value:335, name:'直接访问'},
                {value:310, name:'邮件营销'},
                {value:234, name:'联盟广告'},
                {value:135, name:'视频广告'},
                {value:1548, name:'搜索引擎'}
              ]
          }
      },
      methods:{
        //   go(){
        //     this.$router.push('/echar')
        //   },
          drawPie(id){
              let self = this;
              this.charts = echarts.init(document.getElementById(id))
              this.charts.setOption({
                tooltip: {
                  trigger: 'item',
                //   formatter: '{b}:{c} ({d}%)'
                    formatter: function (params,ticket,callback) {
                        let res = params;
                        // console.log(res)
                        self.code = res.name
                        // for (let i = 0, l = params.length; i < l; i++) {
                        res = res.name + ' : ' + res.data.value;
                        // }
                        return res
                    },
                },
                legend: {
                  orient: '',
                  x: 'left',
                  y:'50',
                  data:this.opinion
                },
                series: [
                  {
                    name:null,
                    type: "pie",
                    radius: "70%",
                    center: ["50%", "40%"],
                    avoidLabelOverlap: false,
                    label: {
                      normal: {
                        show: false, //展示
                        position: "outside" // outside表示文本显示位置为外部
                    },
                      emphasis: {
                            //文本样式
                            show: false, //展示
                            textStyle: {
                            //文本样式
                                fontSize: "14",
                                fontWeight: "600"
                            }
                        }
                    },
                    labelLine: {
                      normal: {
                        show: false
                      }
                    },
                    data:this.opinionData
                  }
                ]
              })
          },
          back(){
            this['$router'].go(-1);
        },
          drawblone(id){
              this.charts = echarts.init(document.getElementById(id))
              this.charts.setOption({
                tooltip: {
                    trigger: "axis",
                    },
                   legend: {
                        data: ["第一季度", "第二季度", "第三季度", "第四季度"]
                    },
                    // x轴
                    xAxis: {
                        data: this.xAxisData
                    },
                    yAxis: {},
                    // 数据
                    series: [
                    {
                        name: "第一季度",
                        type: "bar",
                        barGap: 0,
                        // label: {
                        //     normal: {
                        //         show: true,
                        //         position: 'insideRight',
                        //         formatter: '{c}%'
                        //     }
                        // },
                        data: this.seriesData
                    },
                    {
                        name: "第二季度",
                        type: "bar",
                        barGap: 0,
                        // label: {
                        //     normal: {
                        //         show: true,
                        //         position: 'insideRight',
                        //         formatter: '{c}%'
                        //     }
                        // },
                        data: this.seriesData
                    },
                    {
                        name: "第三季度",
                        type: "bar",
                        barGap: 0,
                        // label: {
                        //     normal: {
                        //         show: true,
                        //         position: 'insideRight',
                        //         formatter: '{c}%'
                        //     }
                        // },
                        data: this.seriesData
                    },
                    {
                        name: "第四季度",
                        type: "bar",
                        barGap: 0,
                        // label: {
                        //     normal: {
                        //         show: true,
                        //         position: 'insideRight',
                        //         formatter: '{c}%'
                        //     }
                        // },
                        data: this.seriesData
                    },
                    ]
              })
          }
      },
      created(){
            // let params;
            // params = this.$route.params;
            // if(params.from) {
            //     sessionStorage.removeItem('echaetsParamsData');
            //     sessionStorage.setItem("echaetsParamsData", JSON.stringify(params)); //把上个页面的路由带过来的参数保存到sessionStorage 
            // } else {
            //     params = JSON.parse(sessionStorage.getItem("echaetsParamsData"));
            // }
            // this.type = params.type;
            // if(params.from === '直接访问') {
            //     this.echartsTitle = '直接访问'
            //     this.opinionData.push({value:335, name:'直接访问'});
            // } else if(params.from === '邮件营销') {
            //     this.echartsTitle = '邮件营销'
            //     this.opinionData.push({value:310, name:'邮件营销'});
            // }else if(params.from === '联盟广告') {
            //     this.echartsTitle = '联盟广告'
            //     this.opinionData.push({value:234, name:'联盟广告'});
            // }else if(params.from === '视频广告') {
            //     this.echartsTitle = '视频广告'
            //     this.opinionData.push({value:135, name:'视频广告'});
            // }else if(params.from === '搜索引擎') {
            //     this.echartsTitle = '搜索引擎'
            //     this.opinionData.push({value:1548, name:'搜索引擎'});
            // }else if(params.from === '广告') {
            //     this.echartsTitle = '广告'
            //     // this.opinionData.push({value:1548, name:'搜索引擎'});
            // }else if(params.from === '商业') {
            //     this.echartsTitle = '商业'
            //     // this.opinionData.push({value:1548, name:'搜索引擎'});
            // }else if(params.from === '视频') {
            //     this.echartsTitle = '视频'
            //     // this.opinionData.push({value:1548, name:'搜索引擎'});
            // }else if(params.from === '食品') {
            //     this.echartsTitle = '食品'
            //     // this.opinionData.push({value:1548, name:'搜索引擎'});
            // }
            // this.opinion.push(this.echartsTitle);
            // this.seriesData.push(params.value);
            // this.xAxisData.push(this.echartsTitle);
    },
    //调用
      mounted(){
          this.$nextTick(function() {
            //   if(this.type === 'pie') {
                  this.drawPie('main')
            //   } else {
                //   this.drawblone('main2')
            //   }
          })
      }
  }
</script>

<style scoped lang="scss">
    .echartsView {
        padding: 20px;
        .echartsItem {
            width: 49%;
            height: 400px;
            padding:10px;
            float: left;
            .echartsBox {
                width: 100%;
                height: 100%;
            }
        }
    }
</style>