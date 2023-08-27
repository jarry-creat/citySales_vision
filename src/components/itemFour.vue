<template>
  <div>
    <h2>产品库存统计图</h2>
    <div id="chartDom" class="chart">

    </div>
  </div>
</template>

<script>
import {inject,onMounted,reactive} from "vue"
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios")
    let data = reactive({})
    async function getState(){
        data = await $http({url:"/four/data"})
    }
    // 1.在dom加载完毕后动态展示图表
    onMounted(()=>{
      getState().then(()=>{
        console.log("柱状图",data);
        let myChart = $echarts.init(document.getElementById("chartDom"));
        myChart.setOption({
          xAxis:{
            axisLine:{
              lineStyle:{
                color:"#fff"
            }
          },
            type:"category",
            data:data.data.chartFour.chartData.day
          },
          yAxis:{
            axisLine:{
              lineStyle:{
                
              }
            },
            type:"value"
          },
          tooltip: {
            trigger: "axis",
            axisPointer: {//设置鼠标选中样式为阴影
              type: "shadow",
            }
          },
          legend: {},//图例
          grid: {//位置
            left: "3%",
            right: "4%",
            bottom: "3%",
            containLabel: true,//设置包含坐标轴
          },
          series:[
          {
            name: "服饰",
            type: "bar",
            data: data.data.chartFour.chartData.num.Chemicals,
            stack: "total",//数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置
            label: {
            //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
            show: true,
            },
            emphasis: {
            //高亮的图形样式和标签样式。
            focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
            },
          },
          {
            name: "数码",
            type: "bar",
            data: data.data.chartFour.chartData.num.Clothes,
            stack: "total",//数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置
            label: {
            //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
            show: true,
            },
            emphasis: {
            //高亮的图形样式和标签样式。
            focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
            },
          },
          {
            name: "家电",
            type: "bar",
            data: data.data.chartFour.chartData.num.Electrical,
            stack: "total",//数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置
            label: {
            //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
            show: true,
            },
            emphasis: {
            //高亮的图形样式和标签样式。
            focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
            },
          },
          {
            name: "家居",
            type: "bar",
            data: data.data.chartFour.chartData.num.digit,
            stack: "total",//数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置
            label: {
            //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
            show: true,
            },
            emphasis: {
            //高亮的图形样式和标签样式。
            focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
            },
          },
          {
            name: "日化",
            type: "bar",
            data: data.data.chartFour.chartData.num.gear,
            stack: "total",//数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置
            label: {
            //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
            show: true,
            },
            emphasis: {
            //高亮的图形样式和标签样式。
            focus: "series", //聚焦当前高亮的数据所在的系列的所有图形。
            },
          },
          ],
        })
      })
    })
    return { getState,data }
  }
}
</script>

<style lang="less">
h2 {
  height: 0.6rem;
  color: #fff;
  line-height: 0.6rem;
  text-align: center;
  font-size: 0.25rem;
}
.chart {
/* 高度360 */
height: 4.5rem;
}
</style>