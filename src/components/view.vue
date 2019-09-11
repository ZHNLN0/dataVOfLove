<template>
  <div class="container">
    <div class="headerLeft"></div>
    <div class="headerCenter"></div>
    <div class="headerRight"></div>
    <div class="title">连接嗅探</div>
    <div class="leftContainer">
      <div class="title">
        连接嗅探连接嗅探
      </div>
      <countTo class="countTo" :startVal="startVal" :endVal="endVal" :duration="1000"></countTo>
      <div class="ringChart" ref="ring"></div>
    </div>
    <div class="centerContainer">
      <div class="title">词云</div>
      <div class="wordCloud" ref="word"></div>
    </div>
    <div class="rightContainer">
      <div class="title">七天小结</div>
      <div class="barChart" ref="bar"></div>
    </div>
    <div class="bottomContainer" ref="discount"></div>
    <div class="word">
      再看左边, &nbsp; &nbsp; --->> <br> <span style="font-weight: 600;color: yellow;">看左边看左边看左边</span> 
    </div>
  </div>
</template>

<script>
import countTo from 'vue-count-to'
var echart = require('echarts');
require('echarts-wordcloud');
require('echarts-liquidfill');
export default {
  name: 'HelloWorld',
  data () {
    return {
      ringChart: null,
      ringData: [
        { value: 1000, name: '嘿嘿嘿'},
        { value: 2000, name: '滴滴滴滴'}
      ],
      wordCloud: null,
      wordCloudData: [
        {
          name: 'Sam S Club',
          value: 10000,
        }, {
            name: 'Macys',
            value: 6181
        }, {
            name: 'Amy Schumer',
            value: 4386
        }, {
            name: 'Jurassic World',
            value: 4055
        }, {
            name: 'Charter Communications',
            value: 2467
        }, {
            name: 'Chick Fil A',
            value: 2244
        }, {
            name: 'Planet Fitness',
            value: 1898
        }, {
            name: 'Pitch Perfect',
            value: 1484
        }, {
            name: 'Express',
            value: 1112
        }, {
            name: 'Home',
            value: 965
        }, {
            name: 'Johnny Depp',
            value: 847
        }, {
            name: 'Lena Dunham',
            value: 582
        }, {
            name: 'Lewis Hamilton',
            value: 555
        }, {
            name: 'KXAN',
            value: 550
        }, {
            name: 'Mary Ellen Mark',
            value: 462
        }, {
            name: 'Farrah Abraham',
            value: 366
        }, {
            name: 'Rita Ora',
            value: 360
        }, {
            name: 'Serena Williams',
            value: 282
        }, {
            name: 'NCAA baseball tournament',
            value: 273
        }, {
            name: 'Point',
            value: 273
        }, {
            name: 'Point Break',
            value: 265
        },{
        name: "Jayfee",
        value: 666
        }, {
            name: "Nancy",
            value: 520
        }, {
            name: "生活资源",
            value: "999"
        }, {
            name: "供热管理",
            value: "888"
        }, {
            name: "供气质量",
            value: "777"
        }, {
            name: "生活用水管理",
            value: "688"
        }, {
            name: "一次供水问题",
            value: "588"
        }, {
            name: "交通运输",
            value: "516"
        }, {
            name: "城市交通",
            value: "515"
        }, {
            name: "环境保护",
            value: "483"
        }, {
            name: "房地产管理",
            value: "462"
        }, {
            name: "城乡建设",
            value: "449"
        }, {
            name: "社会保障与福利",
            value: "429"
        }, {
            name: "社会保障",
            value: "407"
        }, {
            name: "文体与教育管理",
            value: "406"
        }, {
            name: "公共安全",
            value: "406"
        }, {
            name: "公交运输管理",
            value: "386"
        }, {
            name: "出租车运营管理",
            value: "385"
        }, {
            name: "供热管理",
            value: "375"
        }, {
            name: "市容环卫",
            value: "355"
        }, {
            name: "自然资源管理",
            value: "355"
        }, {
            name: "粉尘污染",
            value: "335"
        }, {
            name: "噪声污染",
            value: "324"
        }, {
            name: "土地资源管理",
            value: "304"
        }, {
            name: "物业服务与管理",
            value: "304"
        }, {
            name: "医疗卫生",
            value: "284"
        }, {
            name: "粉煤灰污染",
            value: "284"
        }, {
            name: "占道",
            value: "284"
        }, {
            name: "供热发展",
            value: "254"
        }, {
            name: "农村土地规划管理",
            value: "254"
        }, {
            name: "生活噪音",
            value: "253"
        }, {
            name: "供热单位影响",
            value: "253"
        }, {
            name: "城市供电",
            value: "223"
        }, {
            name: "房屋质量与安全",
            value: "223"
        }, {
            name: "大气污染",
            value: "223"
        }, {
            name: "房屋安全",
            value: "223"
        }, {
            name: "文化活动",
            value: "223"
        }, {
            name: "拆迁管理",
            value: "223"
        }, {
            name: "公共设施",
            value: "223"
        }, {
            name: "供气质量",
            value: "223"
        }, {
            name: "供电管理",
            value: "223"
        }, {
            name: "燃气管理",
            value: "152"
        }, {
            name: "教育管理",
            value: "152"
        }, {
            name: "医疗纠纷",
            value: "152"
        }, {
            name: "执法监督",
            value: "152"
        }, {
            name: "设备安全",
            value: "152"
        }, {
            name: "政务建设",
            value: "152"
        }, {
            name: "县区、开发区",
            value: "152"
        }, {
            name: "宏观经济",
            value: "152"
        }, {
            name: "教育管理",
            value: "112"
        }, {
            name: "社会保障",
            value: "112"
        }, {
            name: "生活用水管理",
            value: "112"
        }, {
            name: "物业服务与管理",
            value: "112"
        }, {
            name: "分类列表",
            value: "112"
        }, {
            name: "农业生产",
            value: "112"
        }, {
            name: "二次供水问题",
            value: "112"
        }, {
            name: "城市公共设施",
            value: "92"
        }, {
            name: "拆迁政策咨询",
            value: "92"
        }, {
            name: "物业服务",
            value: "92"
        }, {
            name: "物业管理",
            value: "92"
        }, {
            name: "社会保障保险管理",
            value: "92"
        }, {
            name: "低保管理",
            value: "92"
        }, {
            name: "文娱市场管理",
            value: "72"
        }, {
            name: "城市交通秩序管理",
            value: "72"
        }, {
            name: "执法争议",
            value: "72"
        }, {
            name: "商业烟尘污染",
            value: "72"
        }, {
            name: "占道堆放",
            value: "71"
        }, {
            name: "地上设施",
            value: "71"
        }, {
            name: "水质",
            value: "71"
        }, {
            name: "无水",
            value: "71"
        }, {
            name: "供热单位影响",
            value: "71"
        }, {
            name: "人行道管理",
            value: "71"
        }, {
            name: "主网原因",
            value: "71"
        }, {
            name: "集中供热",
            value: "71"
        }, {
            name: "客运管理",
            value: "71"
        }, {
            name: "国有公交（大巴）管理",
            value: "71"
        }, {
            name: "工业粉尘污染",
            value: "71"
        }, {
            name: "治安案件",
            value: "71"
        }, {
            name: "压力容器安全",
            value: "71"
        }, {
            name: "身份证管理",
            value: "71"
        }, {
            name: "群众健身",
            value: "41"
        }, {
            name: "工业排放污染",
            value: "41"
        }, {
            name: "破坏森林资源",
            value: "41"
        }, {
            name: "市场收费",
            value: "41"
        }, {
            name: "生产资金",
            value: "41"
        }, {
            name: "生产噪声",
            value: "41"
        }, {
            name: "农村低保",
            value: "41"
        }, {
            name: "劳动争议",
            value: "41"
        }, {
            name: "劳动合同争议",
            value: "41"
        }, {
            name: "劳动报酬与福利",
            value: "41"
        }, {
            name: "医疗事故",
            value: "21"
        }, {
            name: "停供",
            value: "21"
        }, {
            name: "基础教育",
            value: "21"
        }, {
            name: "职业教育",
            value: "21"
        }, {
            name: "物业资质管理",
            value: "21"
        }, {
            name: "拆迁补偿",
            value: "21"
        }, {
            name: "设施维护",
            value: "21"
        }, {
            name: "市场外溢",
            value: "11"
        }, {
            name: "占道经营",
            value: "11"
        }, {
            name: "树木管理",
            value: "11"
        }, {
            name: "农村基础设施",
            value: "11"
        }, {
            name: "无水",
            value: "11"
        }, {
            name: "供气质量",
            value: "11"
        }, {
            name: "停气",
            value: "11"
        }, {
            name: "市政府工作部门（含部门管理机构、直属单位）",
            value: "11"
        }, {
            name: "燃气管理",
            value: "11"
        }, {
            name: "市容环卫",
            value: "11"
        }, {
            name: "新闻传媒",
            value: "11"
        }, {
            name: "人才招聘",
            value: "11"
        }, {
            name: "市场环境",
            value: "11"
        }, {
            name: "行政事业收费",
            value: "11"
        }, {
            name: "食品安全与卫生",
            value: "11"
        }, {
            name: "城市交通",
            value: "11"
        }, {
            name: "房地产开发",
            value: "11"
        }, {
            name: "房屋配套问题",
            value: "11"
        }, {
            name: "物业服务",
            value: "11"
        }, {
            name: "物业管理",
            value: "11"
        }, {
            name: "占道",
            value: "11"
        }, {
            name: "园林绿化",
            value: "11"
        }, {
            name: "户籍管理及身份证",
            value: "11"
        }, {
            name: "公交运输管理",
            value: "11"
        }, {
            name: "公路（水路）交通",
            value: "11"
        }, {
            name: "房屋与图纸不符",
            value: "11"
        }, {
            name: "有线电视",
            value: "11"
        }, {
            name: "社会治安",
            value: "11"
        }, {
            name: "林业资源",
            value: "11"
        }, {
            name: "其他行政事业收费",
            value: "11"
        }, {
            name: "经营性收费",
            value: "11"
        }, {
            name: "食品安全与卫生",
            value: "11"
        }, {
            name: "体育活动",
            value: "11"
        }, {
            name: "有线电视安装及调试维护",
            value: "11"
        }, {
            name: "低保管理",
            value: "11"
        }, {
            name: "劳动争议",
            value: "11"
        }, {
            name: "社会福利及事务",
            value: "11"
        }, {
            name: "一次供水问题",
            value: "11"
        }
      ],
      barChart: null,
      discountChart: null,
      timerDiscountData: null,
      timerDiscount: null,
      timerAdd: null,
      xData: [],
      yData: [],
      startVal: 234,
      endVal: 240
    }
  },
  components: {
    countTo
  },
  beforeMount() {
    this.setDiscountData()
    this.add()
  },
  mounted() {
    this.initRingChart()
    this.initWordCloud()
    this.initBarChart()
    this.timerDiscount = setInterval(this.initDiscountChart,1000)
  },
  beforeDestroy() {
    this.timerDiscountData = null,
    this.timerDiscount = null,
    this.timerAdd = null
  },
  methods: {
    initRingChart() {
      let options = {
        legend: {
          type:"plain",
          orient: 'vertical',
          left:'75%',
          align:'left',
          top:'40%',
          itemWidth: 20,
          textStyle: {
              color:'#8C8C8C'
          },
          height:200
        },
        color: ['#094975', '#022c4c'],
        tooltip: {
          show: false
        },
        series: [
          {
            type: 'pie',
            radius: ['60%', '80%'],
            center: ['40%', '50%'],
            label: {
              show: false
            },
            itemStyle: {
              borderColor: '#fff'
            },
            data: this.ringData
          },
          {
            type: 'liquidFill',
            radius: '59%',
            itemStyle: {
                normal: {
                    opacity: 0.4,
                    shadowBlur: 0,
                    shadowColor: 'blue'
                }
            },
            data: [{
                value: 0.3,
                itemStyle: {
                    normal: {
                        color: '#094975',
                        opacity: 0.6
                    }
                }
            }],
            color: ['#53d5ff'],
            center: ['40%', '50%'],
            backgroundStyle: {
                color: '#028ebb'
            },
            label: {
              normal: {
                formatter: function() {
                  return '今日完成进度 \n' + 0.3 *100 + '%' 
                },
                textStyle: {
                    fontSize: 20
                }
              }
            },
            outline: {
                itemStyle: {
                    borderColor: '#86c5ff',
                    borderWidth: 0
                },
                borderDistance: 0
            }
        },
        ]
      }
      this.ring = echart.init(this.$refs.ring)
      this.ring.setOption(options)
    },
    initWordCloud() {
      let options = {
        series: [
          {
            type: 'wordCloud',
            name: '词云',
            autoSize: {
              enable: true,
              minSize: 10
            },
            shape: 'diamond',
            width: '100%',
            height: '100%',   
            gridSize: 8,
            rotationStep: 20,
            sizeRange: [15, 80],
            rotationRange: [-90, 90],
            drawOutOfBound: false,
            textPadding: 0,
            textStyle: {
              normal: {
                fontWeight: 'bold',
                color: function() {
                  return 'rgb(' + [Math.round(Math.random() * 256),Math.round(Math.random() * 256),Math.round(Math.random() * 256)].join(',') + ')'
                }
              }
            },
            data: this.wordCloudData
          }
        ]
      }
      this.wordCloud = echart.init(this.$refs.word)
      this.wordCloud.setOption(options)
      
    },
    initBarChart() {
      let options = {
        tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            },
            textStyle: {
              align: 'left',
              color: '#5cc1ff',
              fontSize: '16'
            },
            borderWidth: '1',
            formatter: '{b}\n{c}'
        },
        label: {
            normal: {
              textStyle: {
                color: "#cccccc"
              }
            },
            emphasis: {
              textStyle: {
                color: "#cccccc"
              }
            }
        },
        grid: {
          left: '10%',
          right: '10%',
          bottom: '10%',
          top: '50',
          containLabel: true
        },
        yAxis: {
          type: 'category',
          axisLine: {
            show:false,
            lineStyle: {
              color: '#8ac7ff'
            }
          },
          axisTick: {
            show: false,
            interval: 0,
            alignWithLabel: true
          },
          axisLabel: {
            interval: 0,
            rotate: '0',
            textStyle: {
              fontSize: 15,
              color: '#cee8ff'
            }
          },
          data: ['七天前', "六天前",'五天前', '四天前', "大前天", '前天', "昨天"],
          splitLine: {
            show: false
          }
        },
        xAxis: {
            type: 'value',
            name: '',
            splitLine: {
              show: false,
              lineStyle: {
                color: ['rgba(138, 199, 255, .2)']
              }
            },
            axisTick: {
              show: false
            },
            axisLabel: {
              show: false
            },
            axisLine: {
              show:false,
              lineStyle: {
                color: '#01c2db'
              }
            }
        },
        series: [{
            name: '数量',
            type: 'bar',
            stack: '总量',
            barWidth: 15,
            label: {
              normal: {
                show: true,
                color:'#fff',
                position: 'right',
                formatter: "{c}"
              }
            },
            itemStyle: {
                normal: {
                  barBorderWidth: '0',
                  barBorderRadius: [10, 10, 10, 10],
                  barBorderColor: 'rgb(9,73,117)',
                  color: new echart.graphic.LinearGradient(0, 0, 1, 0, [{
                    offset: 0,
                    color: 'rgba(9,73,117, .4)'
                  }, {
                    offset: 1,
                    color: 'rgb(9,73,117)' 
                  }])
                },
                emphasis: {
                  barBorderWidth: '1',
                  barBorderColor: 'rgb(9,73,117)'
                }
            },
            data: [700, 790, 1250, 1278, 1600, 1820, 2335]
        }]
      }
      this.barChart = echart.init(this.$refs.bar)
      this.barChart.setOption(options)
    },
    initDiscountChart() {
      this.discountChart = echart.init(this.$refs.discount)
      let options = {
        color: [ '#0099ff'],
        tooltip: {
          trigger: 'axis'
        },
        grid: {
          left: '5%',
          right: '5%',
          bottom: '5%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            boundaryGap: ['10%', '10%'],
            axisTick: {
              alignWithLabel: true
            },
            axisLine: {
              lineStyle: {
                color: '#bfbfbf'
              }
            },
            axisLabel: {
              color: '#545454',
              margin: 15
            },
            data: this.xData
          }
        ],
        yAxis: [{
          type: 'value',
          scale: true,
          splitNumber: 3,
          axisLine: {
            show: false,
          },
          axisLabel: {
            color: '#545454',
            margin: 10
          },
          splitLine: {
            lineStyle: {
            type: 'dashed'
            },
          },
          axisTick: {
            show: false
          }
        }],
        series: [
          {
            name: '网络出口流量',
            type: 'line',
            stack: '总量',
            showSymbol: false,
            lineStyle: {
              color: '#09f'
            },
            areaStyle: {
              color: '#09f',
              opacity: 0.5
            },
            data: this.yData
          }
        ]
      }
      this.discountChart.setOption(options)
      window.addEventListener('resize', () => {
        console.log('stack')
        setTimeout(this.stacked.resize, 200)
      })
    },
    setDiscountData() {
      let now = new Date();
      let y = Math.round(Math.random() * 10)
      this.xData.push(now.toLocaleTimeString().replace(/^\D*/, ''))
      this.yData.push(y)
      if(this.xData.length == 15) {
        this.xData.shift()
        this.yData.shift()
      }
      this.timerDiscountData = setTimeout(
        this.setDiscountData
      , 1000);
    },
    add() {
      this.startVal = this.endVal;
      this.endVal += Math.random() * 10
      this.timerAdd = setTimeout(this.add, 2000)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus">
@import '../common/mixin.styl'
  .container
    width 1920px
    height 1080px
    background-color #090c2b
    color #ffffff
    .headerLeft
      width 368px
      height 27px
      LT(143px, 62px)
      bg-image('../assets/u83.png')
    .headerCenter
      width 738px
      height 92px
      LT(575px, 30px)
      bg-image('../assets/u1.png')
    .headerRight
      width 368px
      height 27px
      RT(143px, 62px)
      bg-image('../assets/u84.png')
    .title 
      width 948px
      height 64px
      fontStyle(50px, center, 64px)
      LT(480px, 60px)
    .leftContainer
      width 400px
      height 550px
      overflow hidden
      LT(100px, 200px)
      .title
        width 400px
        height 100px
        font-weight 700
        LT(0px, 0px)
        fontStyle(50px, center, 100px)
      .countTo
        width 400px
        height 200px
        font-weight 600
        LT(0px, 100px)
        fontStyle(50px, center, 200px)
      .ringChart
        width 400px
        height 250px
        LT(0px, 300px)
    .centerContainer
      width 800px
      height 550px
      LT(560px, 200px)
      .title
        width 800px
        height 100px
        font-weight 700
        LT(0px, 0px)
        fontStyle(50px, center, 100px)
      .wordCloud
        width 800px
        height 450px
        LT(0px, 100px)
    .rightContainer
      width 400px
      height 550px
      RT(100px, 200px)
      .title
        width 400px
        height 100px
        font-weight 700
        LT(0px, 0px)
        fontStyle(50px, center, 100px)
      .barChart
        width 400px
        height 450px
        LT(0px, 100px)
    .bottomContainer
      width 1200px
      height 280px
      LT(500px, 780px)
    .word
      width 400px
      height 200px
      LT(100px, 850px)
      fontStyle(40px, left, 60px)
</style>
