<template>
    <div :class="className" :style="{ height: height, width: width }" />
</template>

<script>
import echarts from "echarts";
require("echarts/theme/macarons"); // echarts theme
import resize from "./mixins/resize";
import { color } from "echarts/lib/export";


var str = "数据库资源占用";
var sjk = "40%";



export default {
    mixins: [resize],
    props: {
        className: {
            type: String,
            default: "chart",
        },
        width: {
            type: String,
            default: "100%",
        },
        height: {
            type: String,
            default: "300px",
        },
    },
    data() {
        return {
            chart: null,
        };
    },
    mounted() {
        this.$nextTick(() => {
            this.initChart();
        });
    },
    beforeDestroy() {
        if (!this.chart) {
            return;
        }
        this.chart.dispose();
        this.chart = null;
    },
    methods: {
        initChart() {
            this.chart = echarts.init(this.$el, "macarons");
            this.chart.setOption({
                tooltip: {
                    trigger: "item",
                    formatter: "{a} <br/>{b} : {c} ({d}%)",
                },
                legend: {
                    left: "center",
                    bottom: "10",
                    data: [],
                },
                graphic: [{
                    silent: true,
                    type: 'text',//控制内容为文本文字
                    left: 'center',
                    top: '40%',//调整距离盒子高处的位置
                    style: {
                        fill: 'green',//控制字体颜色
                        text: str,//控制第一行字显示内容
                        fontSize: '16',
                    }
                }, {
                    silent: true,
                    type: 'text',
                    left: 'center',
                    top: '55%',
                    z: 10,
                    style: {
                        text: sjk,
                        font: 'Microsoft YaHei',
                        fontSize: '32',
                        lineHeight: 15,
                        fill: 'red',
                    }
                }],
                series: [
                    {
                        name: "数据库资源占用",
                        type: "pie",
                        //roseType: "radius",//改变粗细 
                        radius: ["50%", "66%"],
                        center: ["50%", "50%"],
                        //silent: "false", //鼠标事件 反向true
                        avoidLabelOverlap: false,
                        label: {
                            show: false,
                            position: 'center'
                        },
                        /* emphasis: {
                            label: {
                                show: true,
                                fontSize: 20,
                                fontWeight: 'bold'
                            }
                        }, */
                        data: [
                            {
                                value: 60,
                                name: "空间占用",
                                itemStyle: {
                                    color: "#F0FFF0",
                                    normal: {
                                        borderColor: {
                                            colorStops: [
                                                {
                                                    offset: 0,
                                                    color: "#F0FFF0" // 0% 处的颜色
                                                },
                                                {
                                                    offset: 0.5,
                                                    color: "#4ec7e1" // 0% 处的颜色
                                                },
                                                {
                                                    offset: 1,
                                                    color: "#C2FFC2" // 100% 处的颜色
                                                }
                                            ]
                                        },
                                        color: {
                                            // 完成的圆环的颜色
                                            colorStops: [
                                                {
                                                    offset: 0,
                                                    color: "#F0FFF0" // 0% 处的颜色
                                                },
                                                {
                                                    offset: 0.5,
                                                    color: "#4ec7e1" // 50% 处的颜色

                                                },
                                                {
                                                    offset: 1,
                                                    color: "#C2FFC2" // 100% 处的颜色
                                                }
                                            ]
                                        },
                                        label: {
                                            show: false
                                        }
                                    }
                                }
                            },
                            {
                                name: "剩余空间",
                                value: 40,
                                itemStyle: { color: "#E1FFE1" },
                            },
                        ],

                        animationEasing: "cubicInOut",
                        animationDuration: 2600,
                    },
                ],
            });
        },
    },
};
</script>
