<template>
    <div>
      <h2>基本销售总量</h2>
      <div class="chart" id="oneChart">    
      </div>
    </div>
  </template>
  
  <script>
  import {inject,onMounted,reactive} from "vue"
  export default {
    setup() {
      let $echarts =  inject("echarts") // 得到echarts对象
      let $http = inject("axios")

      let data = reactive({})
      let xdata = reactive([])
      let ydata = reactive([])
      function setData() {
        xdata = data.data.chartOne.chartData.map(v=>v.title)
        ydata = data.data.chartOne.chartData.map(v=>v.num)
        console.log("xdata",xdata)
        console.log("ydata",ydata)
      }
      async function getState() {
        data = await $http({url:"/one/data"})
        // console.log(oneData.data.chartOne.chartData)
      }
      onMounted(()=>{
        let myChart =  $echarts.init(document.getElementById("oneChart"))
        // 调用请求
         getState().then(()=>{
          setData(),
          myChart.setOption({
            grid:{
              top: "3%",
              left: "1%",
              right: "6%",
              bottom: "3%",
              containLabel:true
            },
            xAxis: {
              type:"value"
            },
            yAxis: {
              type:"category",
              data:xdata
            },
            series:[{
              type:"bar",
              data:ydata,
              itemStyle: {
                normal:{
                  barBorderRadius: [0,20,20,0],
                  color: new $echarts.graphic.LinearGradient(0,0,1,0,[
                    {
                      offset:0,
                      color:"#005eaa",
                    },
                    {
                      offset:0.5,
                      color:"#339ca8",
                    },
                    {
                      offset: 1,
                      color: "#cda819"
                    }
                  ])
                }
              }
            }
          ]
         })
         });
      })
      return {
        getState,data,xdata,ydata,setData
      }
    }
  }
  </script>
  
<style scoped>
.chart {
  height: 4.5rem;
}
h2 {
  height: .6rem;
  color:#fff;
  line-height:.6rem;
  font-size:.25rem;
  text-align:center
}
</style>