<template>
  <div class="time-statistics">
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
      <dl class='all'>
        <dt>전체</dt>
        <dd>
          <span>
            <label>이용횟수</label>
            <strong>75</strong>
          </span>
          <span>
            <label>이용금액</label>
            <strong>453,000원</strong>
          </span>
        </dd>
      </dl>
      <dl>
        <dt>가장 이용이 많은 월</dt>
        <dd>
          <span>
            <label>기간</label>
            <strong>8월</strong>
          </span>
          <span>
            <label>이용횟수</label>
            <strong>781</strong>
          </span>
          
        </dd>
      </dl>
      <dl>
        <dt>가장 이용이 적은 월</dt>
        <dd>
          <span>
            <label>기간</label>
            <strong>2월</strong>
          </span>
          <span>
            <label>이용횟수</label>
            <strong>594</strong>
          </span>
        </dd>
      </dl>
      <dl>
        <dt>세탁기 전체</dt>
        <dd>
          <span>
            <label>이용횟수</label>
            <strong>523</strong>
          </span>
          <span>
            <label>이용금액</label>
            <strong>1,584,800원</strong>
          </span>
        </dd>
      </dl>
      <dl>
        <dt>건조기 전체</dt>
        <dd>
          <span>
            <label>이용횟수</label>
            <strong>431</strong>
          </span>
          <span>
            <label>이용금액</label>
            <strong>1,251,000원</strong>
          </span>
        </dd>
      </dl>
      <dl>
        <dt>기타장비 전체</dt>
        <dd>
          <span>
            <label>이용횟수</label>
            <strong>135</strong>
          </span>
          <span>
            <label>이용금액</label>
            <strong>347,000원</strong>
          </span>
        </dd>
      </dl>
    </div>

    <v-row>
      <v-col cols="9">
        <div class="lineChart">
          <BarChart :chartData="chart"/>
        </div>
      </v-col>
      <v-col cols="3">
        <div class="pieChart">
          <PieChart :chartData="pieChart"/>
        </div>
      </v-col>
    </v-row>      

    <div class="dataTable">
      <table cellpadding="0" cellspacing="0">
        <thead>
          <tr>
            <th rowspan="2">기간</th>
            <th colspan="2" class="total">전체</th>
            <th colspan="2">세탁기</th>
            <th colspan="2">건조기</th>
            <th colspan="2">기타장비</th>
          </tr>
          <tr>
            <th class="total">이용횟수</th>
            <th class="total">매출액</th>
            <th>이용횟수</th>
            <th>매출액</th>
            <th>이용횟수</th>
            <th>매출액</th>
            <th>이용횟수</th>
            <th>매출액</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1월</td>
            <td class="total">481</td>
            <td class="total">5,340,000원</td>
            <td>343</td>
            <td>986,000원</td>
            <td>300</td>
            <td>894,000원</td>
            <td>34</td>
            <td>164,000원</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import LineChart from '@/components/lineChart.vue';
import OptionBox from '@/components/optionBox.vue';
import PieChart from '@/components/pieChart.vue';
import BarChart from '@/components/barChart.vue';


export default {
  components:{
    LineChart, OptionBox, PieChart, BarChart
  },

  data() {
    return {
      date: new Date().toISOString().substr(0, 4),
      menu: false,

      chart:{
        chartdata: {
          labels: ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월'],
          datasets: [
            {
              label: '세탁기',
              backgroundColor:'rgba(0,150,255,1)',
              barPercentage:0.3,
              data: [343,318,422,348,541,481,362,618,521,484,321,600],
            },
            {
              label: '건조기',
              backgroundColor:'rgba(255,0,110,1)',
              barPercentage:0.3,
              data: [300,12,34,151,345,332,241,151,61,45,185,112],
            },
            {
              label: '기타장비',
              backgroundColor:'rgba(131,56,236,1)',
              barPercentage:0.3,
              data: [34,64,54,32,120,84,64,87,15,45,32,24],
            },
          ]
        },
        
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales:{
            yAxes:[{
              stacked:true
            }],
            xAxes:[{
              stacked:true
            }]
          }
        }
      },

      pieChart:{
        chartdata:{
          labels:['세탁기','건조기','기타장비'],
          datasets:[
            {
              backgroundColor:['rgba(0,150,255,1)','rgba(255,0,110,1)','rgba(131,56,236,1)'],
              borderWidth:5,
              data:[63,29,8]
            },
          ]
        },


        options: {
          responsive: true,
          maintainAspectRatio: false,
          title:{
            display:true,
            text:'전체 매출 장비별비율'
          },
          showAllTooltips: true,
          layout:{
            padding:{
              top:20,
              left:20,
              right:20,
              bottom:20,
            }
          },
        }
      }
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
.time-statistics{
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
      max-width:280px;
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

      tbody{
        tr:first-child{
          td{border-top:1px solid #ccc;}
        }
      }

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

  .pieChart{
    border:1px solid #e2e2e2;
  }


}
</style>