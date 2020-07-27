<template>
  <div class="statistics">

    <div class="search-opt">
      <table cellpadding="0" cellspacing="0">
        <tr>
          <th>기간검색</th>
          <td>
            <v-btn @click="dateBefor()" icon>
              <v-icon>mdi-chevron-left</v-icon>
            </v-btn>
            <h4>{{this.date}}</h4>
            
            <v-btn @click="dateAfter()" icon>
              <v-icon>mdi-chevron-right</v-icon>
            </v-btn>
          </td>
        </tr>
      </table>
    </div>
    <div class="total-info">
      <dl class="all">
        <dt>나의매장 평균매출</dt>
        <dd>
          <span>
            <label>일 평균매출</label>
            <strong>55,000원</strong>
          </span>
          <span>
            <label>주 평균매출</label>
            <strong>453,000원</strong>
          </span>
          <span>
            <label>월 평균매출</label>
            <strong>3,483,000원</strong>
          </span>
        </dd>
      </dl>
      <dl>
        <dt>나의매장 월평균비용</dt>
        <dd>
          <span>
            <label>월 평균비용</label>
            <strong>3,483,000원</strong>
          </span>
        </dd>
      </dl>
    </div>
    
    <BarChart :chartData="chart"/>

    <div class="dataTable">
      <table cellpadding="0" cellspacing="0">
        <tr>
          <th>기간</th>
          <th class="total">순수익</th>
          <th>총매출</th>
          <th>총비용</th>
          <th>월세</th>
          <th>가스비</th>
          <th>수도세</th>
          <th>전기세</th>
          <th>인터넷/TV</th>
          <th>비품</th>
        </tr>
        <tr>
          <td>1월</td>
          <td class="total">2,807,000원</td>
          <td>3,348,000원</td>
          <td>787,000원</td>
          <td>350,000원</td>
          <td>350,000원</td>
          <td>120,000원</td>
          <td>50,000원</td>
          <td>74,000원</td>
          <td>24,000원</td>
        </tr>
        <tr>
          <td>2월</td>
          <td class="total">2,807,000원</td>
          <td>3,348,000원</td>
          <td>787,000원</td>
          <td>350,000원</td>
          <td>350,000원</td>
          <td>120,000원</td>
          <td>50,000원</td>
          <td>74,000원</td>
          <td>24,000원</td>
        </tr>
      </table>
    </div>

  </div>
</template>

<script>
import BarChart from '@/components/barChart.vue';
import OptionBox from '@/components/optionBox.vue';

export default {
  components:{
    BarChart, OptionBox
  },

  data() {
    return {
      date: new Date().toISOString().substr(0, 4),
      menu: false,

      chart:{
        chartdata: {
          labels: ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월',],
          datasets: [
            {
              label: '나의 매장 월 매출',
              backgroundColor:'rgba(1,161,221,0.15)',
              data: [248000,110000,325000,103000,99000,89000,87000,64500,45000,85000,234000,120000],
            },
            {
              label: '나의 매장 월 비용 ',
              backgroundColor:'rgba(210,10,10,0.15)',
              data: [34000,15000,34000,43000,15000,34000],
            },
          ]
        },
        
        options: {
          tooltips:{

          },
          responsive: true,
          maintainAspectRatio:false,
          scales:{
            yAxes:[{
              ticks:{
                beginAtZero:false, // 눈금자 시작을 0을 포함할것인가?
                stacked:false,
              },
            }],
            xAxes:[{
              ticks:{
                beginAtZero:false,
              }
            }]
          }
        }
      },    
    }
  },

  methods:{
    dateAfter(){
      const dateNumber = Number(this.date)
      this.date = dateNumber + 1
    },
    dateBefor(){
      const dateNumber = Number(this.date)
      this.date = dateNumber - 1
    }
  }
  
}
</script>

<style lang="scss" scoped>
.statistics{

  .search-opt{
    margin-bottom:40px;
    table{
      width:100%;
      border:1px solid #e2e2e2;
      th{
        width:120px;
        padding:15px;
        text-align:center;
        font-size:14px;
      }
      td{
        h4{display:inline-block;margin:0 20px}
      }
    }
  }

  .total-info{
    display:flex;
    margin-bottom:40px;
    border:1px solid #e2e2e2;
    background:#f8f8f8;

    dl{
      border-right:1px solid #e2e2e2;
      flex:1;
      max-width:250px;
      background:#fff;

      dt{
        padding:15px;
        font-size:14px;
        font-family:'SCDream';
        text-align:center;
        border-bottom:1px solid #e2e2e2;
      }
      dd{
        padding:15px;
        text-align:center;
        span{
          display:flex;
          flex-direction: row;
          justify-content: space-between;
          align-items: center;
          font-size:13px;
          margin-bottom:5px;
          label{color:#888}
          strong{}

        }
        span:last-child{margin-bottom:0px;}
      }
    }
    dl.all{
      dt{background:rgba(210,10,10,0.05)}
    }
  }

  .dataTable{
    margin-top:80px;
    table{
      border:1px solid #e2e2e2;
      border-right:0px;
      border-bottom:0px;
      font-size:13px;
      width:100%;
      th{
        border-bottom:1px solid #e2e2e2;
        border-right:1px solid #e2e2e2;
        background:#f8f8f8;
      }
      td{
        text-align:center;
        border-right:1px solid #e2e2e2;
        border-bottom:1px solid #e2e2e2;
      }
      th,td{
        padding:10px;
      }
      th.total{
        background:rgba(210,10,10,0.05);
      }
      td.total{
        font-weight:bold;
        color:#d22828;
      }

      div{
        display:flex;
        align-items: center;
        margin-bottom:5px;

        label{color:#888;font-size:12px;width:60px;text-align:left;}
        span{font-weight:bold;font-size:13px;}
        
      }
      div:last-child{margin-bottom:0px;}
    }
  }


}
</style>