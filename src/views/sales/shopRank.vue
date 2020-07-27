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
        <dt>상위점포(10%) 평균매출</dt>
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
        <dt>하위(10%) 평균매출</dt>
        <dd>
          <span>
            <label>일 평균매출</label>
            <strong>3,500원</strong>
          </span>
          <span>
            <label>주 평균매출</label>
            <strong>154,300원</strong>
          </span>
          <span>
            <label>월 평균매출</label>
            <strong>1,236,000원</strong>
          </span>
        </dd>
      </dl>
    </div>
    
    <LineChart :chartData="chart"/>

    <div class="rankList">
      <v-row>
        <v-col cols="4">
          <div class="rankBox">
            <div class="rankNumber">1위</div>
            <div class="shopInfo">
              <strong>A매장</strong>
              <span>월평균매출: 4,534,000원</span>
            </div>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="rankBox">
            <div class="rankNumber">2위</div>
            <div class="shopInfo">
              <strong>B매장</strong>
              <span>월평균매출: 4,318,000원</span>
            </div>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="rankBox">
            <div class="rankNumber">3위</div>
            <div class="shopInfo">
              <strong>C매장</strong>
              <span>월평균매출: 3,921,000원</span>
            </div>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="rankBox">
            <div class="rankNumber">4위</div>
            <div class="shopInfo">
              <strong>D매장</strong>
              <span>월평균매출: 3,812,000원</span>
            </div>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="rankBox">
            <div class="rankNumber">5위</div>
            <div class="shopInfo">
              <strong>E매장</strong>
              <span>월평균매출: 3,795,000원</span>
            </div>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="rankBox">
            <div class="rankNumber">6위</div>
            <div class="shopInfo">
              <strong>F매장</strong>
              <span>월평균매출: 3,792,000원</span>
            </div>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="rankBox myRank">
            <div class="rankNumber">76위</div>
            <div class="shopInfo">
              <strong>나의 매장</strong>
              <span>월평균매출: 2,426,000원</span>
            </div>
          </div>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
import LineChart from '@/components/lineChart.vue';
import OptionBox from '@/components/optionBox.vue';

export default {
  components:{
    LineChart, OptionBox
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
              label: '전국 매장 월 평균매출',
              borderWidth:1,
              borderColor:'rgba(110,30,232,1)',
              backgroundColor:'rgba(110,30,232,0)',
              data: [323000,300000,290000,280000,270000,260000,250000,240000,230000,132000,340500,240500],
            },
            {
              label: '나의 매장 월 매출',
              borderWidth:1,
              borderColor:'rgba(1,161,221,1)',
              backgroundColor:'rgba(1,161,221,0)',
              data: [248000,110000,325000,103000,99000,89000,87000,64500,45000,85000,234000,120000],
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

  .rankList{
    margin-top:40px;

    .rankBox{
      display:flex;
      padding:15px;
      border:1px solid #e2e2e2;
      .rankNumber{
        display:flex;
        align-items: center;
        justify-content: center;
        width:60px;
        height:60px;
        border-radius:30px;
        background:#f2f2f2;
        font-size:20px;
        font-weight:500;
        font-family:'SCDream';
      }
      .shopInfo{
        display:flex;
        flex-direction: column;
        justify-content: center;
        padding:0 20px;
        strong{display:block;font-size:18px;font-family:'SCDream';font-weight:500}
        span{display:block;color:#888;font-size:14px;margin-top:4px;}
      }
    }
    .myRank{
      border:1px solid #01a1dd;
      .rankNumber{background:#01a1dd;color:#fff;}
      .shopInfo{
        strong{color:#01a1dd;}
        span{color:#292929;}
      }
    }
  }


}
</style>