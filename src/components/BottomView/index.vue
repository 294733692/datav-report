<template>
  <div class="bottom-view">
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="title-wrapper">关键词搜索</div>
        </template>
        <template>
          <div class="chart-wrapper">
            <div class="chart-inner">
              <div class="chart">
                <div class="chart-title">搜索用户数</div>
                <div class="chart-data">93，634</div>
                <v-chart :option="searchUserOption"/>
              </div>
              <div class="chart">
                <div class="chart-title">搜索量</div>
                <div class="chart-data">93，634</div>
                <v-chart :option="searchUserOption"/>
              </div>
            </div>
            <div class="table-wrapper">
              <el-table :data="tableData">
                <el-table-column prop="rank" label="排名" width="180"/>
                <el-table-column prop="keyword" label="关键词" width="180"/>
                <el-table-column prop="count" label="总搜索量"/>
                <el-table-column prop="users" label="搜索用户数"/>
              </el-table>
              <el-pagination
                layout="prev,pager,next"
                :total="100"
                :page-size="pageSize"
                background
                @current-change="onPageChange"
              />
            </div>
          </div>
        </template>
      </el-card>
    </div>
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="title-wrapper">
            <div class="title">分类销售排行</div>
            <div class="radio-wrapper">
              <el-radio-group v-model="radioSelect" size="small">
                <el-radio-button label="品类"></el-radio-button>
                <el-radio-button label="商品"></el-radio-button>
              </el-radio-group>
            </div>
          </div>
        </template>
        <template>
          <div class="chart-wrapper">
            <v-chart :option="categoryOption"></v-chart>
          </div>
        </template>
      </el-card>
    </div>
  </div>
</template>

<script>
export default {
  name: 'index',
  data () {
    return {
      pageSize: 4,
      searchUserOption: {
        xAxis: {
          type: 'category',
          boundaryGap: false
        },
        yAxis: {
          show: false,
          min: 0,
          max: 300
        },
        series: [{
          type: 'line',
          data: [100, 150, 200, 250, 200, 150, 200, 250, 200],
          areaStyle: {
            color: 'rgba(95,187,255,.5)'
          },
          lineStyle: {
            color: 'rgba(95, 187, 255)'
          },
          itemStyle: {
            opacity: 0
          },
          smooth: true
        }],
        grid: {
          top: 0,
          left: 0,
          bottom: 0,
          right: 0
        }
      },
      searchNumberOption: {},
      categoryOption: {},
      tableData: [
        {
          id: 1,
          rank: 1,
          keyword: '北京',
          count: 100,
          users: 90,
          range: 90
        },
        {
          id: 2,
          rank: 2,
          keyword: '北京',
          count: 100,
          users: 90,
          range: 90
        },
        {
          id: 3,
          rank: 3,
          keyword: '北京',
          count: 100,
          users: 90,
          range: 90
        },
        {
          id: 4,
          rank: 4,
          keyword: '北京',
          count: 100,
          users: 90,
          range: 90
        }
      ],
      radioSelect: '品类'
    }
  },
  methods: {
    onPageChange (page) {
      console.log(page)
    },
    renderPieCharts () {
      const mockData = [
        {
          legendName: '粉面粥店',
          value: 67,
          percent: '15.46',
          name: '粉面粥店 | 15.46%',
          itemStyle: {
            color: '#8d7fec'
          }
        },
        {
          legendName: '简餐便当',
          value: 97,
          percent: '22.30',
          name: '简餐便当 | 22.30%',
          itemStyle: {
            color: '#5085f2'
          }
        },
        {
          legendName: '汉堡披萨',
          value: 92,
          percent: '21.15',
          name: '汉堡披萨 | 21.15%',
          itemStyle: {
            color: '#e7e702'
          }
        }
      ]
      this.categoryOption = {
        title: [
          {
            text: '品类分布',
            textStyle: {
              fontSize: 14,
              color: '#666'
            },
            left: 20,
            top: 20
          }, {
            text: '累计订单量',
            subtext: '320',
            textStyle: {
              fontSize: 14,
              color: '#999'
            },
            subtextStyle: {
              fontSize: 28,
              color: '#333'
            },
            x: '34.5%',
            y: '42.5%',
            textAlign: 'center'
          }
        ],
        series: [
          {
            name: '品类分布',
            type: 'pie',
            data: mockData,
            label: {
              normal: {
                show: true,
                position: 'outside',
                formatter: (params) => {
                  return params.data.legendName
                }
              }
            },
            center: ['35%', '50%'],
            radius: ['45%', '60%'], // 圆半径， 内半径，外半径
            labelLine: {
              length: 5,
              length2: 3,
              show: true,
              smooth: true // 绘制线段更加平滑
            },
            clockwise: true, // 顺时针，逆时针排序
            itemStyle: {
              borderWidth: 4,
              borderColor: '#fff'
            }
          }
        ],
        legend: {
          type: 'scroll',
          orient: 'vertical',
          height: 250,
          left: '70%',
          top: 'middle',
          textStyle: {
            color: '#8c8c8c'
          }
        },
        tooltip: {
          trigger: 'item',
          formatter: (params) => {
            const str = params.seriesName + '<br />' +
              params.marker + params.data.legendName + '<br />' +
              '数量：' + params.data.value + '<br />' +
              '占比：' + params.data.percent + '%'
            return str
          }
        }
      }
    }
  },
  mounted () {
    this.renderPieCharts()
  }
}
</script>

<style scoped lang="scss">
.bottom-view {
  display: flex;
  margin-top: 20px;

  .view {
    flex: 1;
    width: 50%;
    box-sizing: border-box;

    &:first-child {
      padding: 0 10px 0 0;
    }

    &:last-child {
      padding: 0 0 0 10px;
    }

    .title-wrapper {
      display: flex;
      align-items: center;
      height: 60px;
      box-sizing: border-box;
      border-bottom: 1px solid #eee;
      font-size: 14px;
      font-weight: 500;
      padding: 0 0 0 20px;

      .radio-wrapper {
        flex: 1;
        display: flex;
        justify-content: flex-end;
        padding-right: 20px;
      }
    }

    .chart-wrapper {
      display: flex;
      flex-direction: column;
      height: 452px;

      .chart-inner {
        display: flex;
        padding: 0 10px;
        margin-top: 20px;

        .chart {
          flex: 1;
          padding: 0 10px;

          .chart-title {
            color: #999;
            font-size: 14px;
          }

          .chart-data {
            font-size: 22px;
            color: #333;
            font-weight: 500;
            letter-spacing: 2px;
          }

          .echarts {
            height: 50px;
          }
        }
      }

      .table-wrapper {
        felx: 1;
        margin-top: 20px;
        padding: 0 20px 20px;

        .el-pagination {
          display: flex;
          justify-content: flex-end;
          margin-top: 15px;
        }
      }
    }
  }
}
</style>
