<template>
  <common-card
    title="累计用户数"
    value="1,107,503">
    <template>
      <v-chart :option="getOptions()"/>
    </template>
    <template v-slot:footer>
      <div class="total-user-footer">
        <span>日同比</span>
        <span class="emphasis">5.14%</span>
        <div class="increase"/>
        <span class="month">月同比</span>
        <span class="emphasis">39.12%</span>
        <div class="decrease"/>
      </div>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from '@/mixins/commonCardMixin'

export default {
  name: 'index',
  mixins: [commonCardMixin],
  methods: {
    getOptions () {
      return {
        grid: {
          left: 0,
          right: 0,
          top: 0,
          bottom: 0
        },
        xAxis: {
          type: 'value',
          show: false
        },
        yAxis: {
          type: 'category',
          show: false
        },
        series: [{
          type: 'bar',
          data: [400],
          stack: '总量',
          barWidth: 10,
          itemStyle: {
            color: '#45c946'
          }
        }, {
          type: 'bar',
          data: [3000],
          stack: '总量',
          itemStyle: {
            color: '#eee'
          }
        }, {
          type: 'custom', // 自定义绘图
          data: [400],
          stack: '总量', // 合并相同名称图形
          renderItem: (params, api) => {
            // console.log(params, api)
            const value = api.value(0) // 获取data中的元素
            const endPoint = api.coord([value, 0]) // 计算坐标位置,数据和坐标关联

            return {
              type: 'group',
              position: endPoint,
              children: [
                {
                  type: 'path',
                  shape: {
                    d: 'M512 640l170.666667-213.333333H341.333333z',
                    x: -5,
                    y: -20,
                    width: 10,
                    height: 10,
                    layout: 'cover' // 指定缩放策略， center 保持原来 pathData 的长宽比，居于矩形中。 cover：拉伸为矩形的长宽比，完全填满矩形
                  },
                  style: {
                    fill: '#45c946' // 填充颜色
                  }
                },
                {
                  type: 'path',
                  shape: {
                    d: 'M512 426.666667l170.666667 213.333333H341.333333z',
                    x: -5,
                    y: 10,
                    width: 10,
                    height: 10,
                    layout: 'cover'
                  },
                  style: {
                    fill: '#45c946' // 填充颜色
                  }
                }
              ]
            }
          }
        }]
      }
    }
  }
}
</script>

<style scoped lang="scss">
.total-user-footer {
  display: flex;
  align-items: center;

  .month {
    margin-left: 10px;
  }
}

</style>
