<template>
  <div>
    <!--面包屑导航区域-->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    </el-breadcrumb>
    <!--卡片视图-->
    <el-card>
      <div id="main" style="width: 750px;height: 400px"></div>
    </el-card>
  </div>
</template>
<script>
import * as echarts from 'echarts'
import _ from 'lodash'
export default {
  data(){
    return{
      //需要合并的数据
      options: {
        title: {
          text: '用户来源'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#E9EEF3'
            }
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            boundaryGap: false
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ]
      }
    }
  },
  created() {
  },
  //此时页面的元素已经渲染完毕
  async mounted() {
    //基于dom，初始化实例
    let myChart=echarts.init(document.getElementById('main'))
    const {data:res}=await this.$http.get('reports/type/1')
    if(res.meta.status!==200){
      return this.$message.error('获取折线图数据失败！')
    }
    //准备数据
    let option = {
      title: {
        text: 'ECharts 入门示例'
      },
      tooltip: {},
      legend: {
        data:['销量']
      },
      xAxis: {
        data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
      },
      yAxis: {},
      series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
      }]
    };
    const result=_.merge(res.data,this.options)
    this.$message.success("成功")
    myChart.setOption(result)
  },
  methods:{}
}

</script>
<style lang="less" scoped>

</style>
