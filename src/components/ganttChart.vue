<template>
<v-chart :options="options"/>
</template>

<style>
/**
 * 默认尺寸为 600px×400px，如果想让图表响应尺寸变化，可以像下面这样
 * 把尺寸设为百分比值（同时请记得为容器设置尺寸）。
 */
/* .echarts {
  width: 100%;
  height: 100%;
} */
</style>

<script>
import echarts from 'vue-echarts'
import 'echarts/lib/chart/line'
import 'echarts/lib/component/polar'

export default {
  components: {
    'v-chart': echarts
  },
  
  data () {

 
var data = [];
// var dataCount = 100;// 测试数据条数
var startTime = 1525835791000; // 2018/5/9 11:16:31
var categories = ['Machine-1', 'Machine-2', 'Machine-3', 'Machine-4'].reverse();
var types = [{
        name: 'Run',
        color: 'green'
    },
    {
        name: 'Idle',
        color: 'yellow'
    },
    {
        name: 'Stop',
        color: 'red'
    },
];

data = [
    {name: 'Run',value: [0, 1525835791000, 1525835791000 + 600000, 600000],itemStyle:{normal: {color: 'green'}}},
    {name: 'Stop',value: [0, 1525836391000, 1525836391000 + 600000, 600000],itemStyle:{normal: {color: 'red'}}},
    {name: 'Run',value: [0, 1525836991000, 1525836991000 + 600000, 600000],itemStyle:{normal: {color: 'green'}}},
    {name: 'Stop',value: [0, 1525837591000, 1525837591000 + 600000, 600000],itemStyle:{normal: {color: 'red'}}},
    
    // value 第一个参数: 设备 index; 
    //       第二个参数: 状态的开始时间; 
    //       第三个参数: 状态的结束时间; 
    //       第四个参数: 状态的持续时间; 
    
    
    {name: 'Run',value: [1, 1525835791000, 1525835791000 + 600000, 600000],itemStyle:{normal: {color: 'green'}}},
    {name: 'Idle',value: [2, 1525836391000, 1525836391000 + 600000, 600000],itemStyle:{normal: {color: 'yellow'}}},
    {name: 'Stop',value: [1, 1525836991000, 1525836991000 + 600000, 600000],itemStyle:{normal: {color: 'red'}}},
    {name: 'Run',value: [3, 1525837591000, 1525837591000 + 600000, 600000],itemStyle:{normal: {color: 'green'}}},
    
    ]
 
 
function renderItem(params, api) {
    var categoryIndex = api.value(0);
    var start = api.coord([api.value(1), categoryIndex]);
    var end = api.coord([api.value(2), categoryIndex]);
    var height = api.size([0, 1])[1] * 0.6;
 
    return {
        type: 'rect',
        shape: echarts.graphic.clipRectByRect({
            x: start[0],
            y: start[1] - height / 2,
            width: end[0] - start[0],
            height: height
        }, {
            x: params.coordSys.x,
            y: params.coordSys.y,
            width: params.coordSys.width,
            height: params.coordSys.height
        }),
        style: api.style()
    };
}
 let options;
options = {
    tooltip: {
        formatter: function(params) {
            // console.log(params)
            return params.marker + params.name + ': ' + params.value[3] / 60000 + ' Min';
        }
    },
    // title: {
    //     text: '设备状态',
    //     left: 'center'
    // },
    legend: {
        data: types,
        bottom: 30,
        right: 20,
        selectedMode: false,
    },
    // dataZoom: [{
    //     type: 'slider',
    //     filterMode: 'weakFilter',
    //     showDataShadow: false,
    //     top: 400,
    //     height: 10,
    //     start: 0,
    //     end: 100, 
    //     borderColor: 'transparent',
    //     backgroundColor: '#e2e2e2',
    //     handleIcon: 'M10.7,11.9H9.3c-4.9,0.3-8.8,4.4-8.8,9.4c0,5,3.9,9.1,8.8,9.4h1.3c4.9-0.3,8.8-4.4,8.8-9.4C19.5,16.3,15.6,12.2,10.7,11.9z M13.3,24.4H6.7v-1.2h6.6z M13.3,22H6.7v-1.2h6.6z M13.3,19.6H6.7v-1.2h6.6z', // jshint ignore:line
    //     handleSize: 20,
    //     handleStyle: {
    //         shadowBlur: 6,
    //         shadowOffsetX: 1,
    //         shadowOffsetY: 2,
    //         shadowColor: '#aaa'
    //     },
    //     labelFormatter: ''
    // }, {
    //     type: 'inside',
    //     filterMode: 'weakFilter'
    // }],
    grid: {
        height: 300
    },
    xAxis: {
        type: 'time',
        min: startTime,
        scale: true,
        // axisLabel: {
        //     formatter: function(val) {
        //         return Math.max(0, val - startTime);
        //     }
        // }
    },
    yAxis: {
        data: categories
    },
    series: [
        {name: types[0].name, type: 'bar', data: [], color: 'red'},
        {name: types[1].name, type: 'bar', data: [], color: 'green'},
        {name: types[2].name, type: 'bar', data: [], color: 'yellow'},
        {
        type: 'custom',
        renderItem: renderItem,
        itemStyle: {
            normal: {
                opacity: 0.8
            }
        },
        encode: {
            x: [1, 2, 3],
            y: 0,
        },
        data: data
    }]
};
    return {options};
  }
}
</script>