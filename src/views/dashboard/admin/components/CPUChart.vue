<template>
  <div :class="className" :style="{ height: height, width: width }" />
</template>

<script>
import echarts from "echarts";
require("echarts/theme/macarons"); // echarts theme
import resize from "./mixins/resize";
import { color } from "echarts/lib/export";

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
      default: "333px",
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
        title: [{
          text: 'CPU占用',
          top: '46%',
          left: '42%',
          textStyle: {
            color: '#000',
            fontSize: 18,

          },
        }
        ],




        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)",
        },
        legend: {
          left: "center",
          bottom: "10",
          data: [],
        },
        series: [
          {
            name: "WEEKLY WRITE ARTICLES",
            type: "pie",
            //roseType: "radius",//改变粗细 
            radius: ["50%", "66%"],
            center: ["50%", "50%"],
            //silent: "false", //鼠标事件 反向true
            data: [
              {
                value: 60,
                name: "CPU占用",
                itemStyle: {

                  color: "#229dfe",
                  normal: {
                    borderColor: {
                      colorStops: [
                        {
                          offset: 0,
                          color: "#229dfe" // 0% 处的颜色
                        },
                        {
                          offset: 0.5,
                          color: "#4ec7e1" // 0% 处的颜色
                        },
                        {
                          offset: 1,
                          color: "#49c3e3" // 100% 处的颜色
                        }
                      ]
                    },
                    color: {
                      // 完成的圆环的颜色
                      colorStops: [
                        {
                          offset: 0,
                          color: "#229dfe" // 0% 处的颜色
                        },
                        {
                          offset: 0.5,
                          color: "#4ec7e1" // 50% 处的颜色

                        },
                        {
                          offset: 1,
                          color: "#49c3e3" // 100% 处的颜色
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
                name: "剩余性能",
                value: 40,
                itemStyle: { color: "#d1d2d4" },
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
