<template>
  <v-dialog
    v-model="state"
    width="900px"
  >
    <div class="pointAll">

      <div class="modal-head">
        <h4>포인트 일괄적립</h4>
      </div>

      <div class="modal-cont">

        <div class="setting">
          <h4><span>Step01</span> 회원 설정</h4>
          <div class="filter-option">
            <dl class="member-number">
              <dt>
                대상회원
              </dt>
              <dd>
                <span>
                  <b>245</b>명
                </span>
              </dd>
            </dl>
            <dl>
              <dt>
                대상회원 설정
              </dt>
              <dd>
                <span><input type="radio" name="select2" value="all" checked v-model="picked"> 전체 가입자</span>
                <span class="bar">
                  |
                </span>
                <span><input type="radio" name="select2" value="befor" v-model="picked"> 회원 가입일 기준</span>
                <span class="bar">
                  |
                </span>
                <span><input type="radio" name="select2" value="after" v-model="picked"> 회원 이용일 기준</span>
              </dd>
            </dl>
            <dl v-if="picked !== 'all'">
              <dt>
                기준날짜
              </dt>
              <dd>
                <span>
                  <v-menu
                      v-model="menu"
                      :close-on-content-click="false"
                      :nudge-right="0"
                      transition="scale-transition"
                      background-color="#fff"
                      offset-y
                    >
                    <template v-slot:activator="{ on }">
                      <v-btn
                        v-model="date"
                        v-on="on"
                        text
                      >
                        {{date}}
                      </v-btn>
                    </template>
                    <v-date-picker
                      v-model="date"
                      :first-day-of-week="1"
                      @input="menu = false"

                    />
                  </v-menu>
                </span>
                <span><input type="radio" name="select"> 이전</span>
                <span class="bar">
                  |
                </span>
                <span><input type="radio" name="select"> 이후</span>
              </dd>
            </dl>
            <dl class="priceInput">
              <dt>
                사용금액 구간
              </dt>
              <dd>
                <span>
                  <input type="text">
                  <label>원</label>
                </span>
                <span>
                  이상 사용자
                </span>
              </dd>
            </dl>
          </div>

          <div class="filter-btn">
            <v-btn outlined>대상 조회하기</v-btn>
          </div>
          
          <h4><span>Step02</span> 적립금 설정</h4>
          <div class="detail-option">
            <dl class="priceInput">
              <dt>적립금액</dt>
              <dd>
                <span>
                  <input type="text">
                  <label>원</label>
                </span>
              </dd>
            </dl>
            <dl>
              <dt>
                적립사유 입력
              </dt>
              <dd>
                <textarea placeholder="적립사유를 입력해주세요"></textarea>
              </dd>
            </dl>
          </div>
        </div>

      </div>

      <div class="footer-btns">
        <v-btn outlined @click="open(false)">
          취소
        </v-btn>
        <v-btn outlined class="ok" @click="$refs.message.open(true)">
          포인트 일괄 지급하기
        </v-btn>
      </div>
    </div>

    <Message ref="message" >
      <template slot="message-cont">
        <div class="message-cont">
          <dl>
            <dt><strong>245명</strong> 회원에게</dt>
            <dd><strong>10,000포인트</strong>를 지급할까요?</dd>
          </dl>
        </div>
      </template>
    </Message>
  </v-dialog>
</template>

<script>
import Message from '@/components/modal/message.vue';

export default {
  components:{
    Message,
  },
  data(){
    return{
      state:false,
      number:0,
      radioGroup: 1,
      date: new Date().toISOString().substr(0, 10),
      menu: false,
      picked:'',
      picked2:'',
    }
  },
  methods:{
    open(value){
      this.state = value;
    }
  }
}
</script>

<style lang="scss" scoped>

.pointAll{
  background:#fff;

  .modal-head{
    padding:0 20px;
    border-bottom:1px solid #e2e2e2;
    height:50px;
    display:flex;
    flex-direction: row;
    align-items: center;

    h4{font-size:18px;font-family:'SCDream';font-weight:500}
  }

  .modal-cont{
    padding:20px;

    .setting{
      flex:1;
    }

    h4{
      font-size:16px;font-family:'SCDream';font-weight:500;margin-bottom:15px;
      span{color:#EE2073;font-size:14px;}
    }


    dl:first-child{border-top:1px solid #292929}
    dl{border-bottom:1px solid #e2e2e2;
      display:flex;
      font-size:14px;
      dt{
        width:150px;background:#f8f8f8;
        display:flex;
        align-items: center;
        padding-left:15px;
        font-family:'SCDream'
      }
      dd{
        flex:1;
        display:flex;
        align-items: center;
        padding:15px;
    
        textarea{
          height:100px;
          min-height:100px;
          max-height:200px;
          width:100%;
          min-width:100%;
          max-width:100%;
          border:1px solid #c2c2c2;
          border-radius:5px;
          padding:10px;
        }

        span{
          display:flex;align-items: center;;margin-right:20px;
          input[type=radio]{width:15px;height:15px;margin-right:5px;}
          input[type=text]{border:1px solid #c2c2c2;height:32px;border-radius:5px;padding:0 5px;padding-right:37px;}
        }

        span.bar{color:#d2d2d2;}
      }
    }

    dl.member-number{
      dd{
        span{
          display:flex;
          align-items: flex-end;

          b{
            color:#EE2073;
            font-size:26px;
            font-family:'SCDream';
            line-height:32px;
            margin-right:5px;
          }
        }
      }
    }

    dl.priceInput{
      dd{
        span{
          position:relative;

          label{position:absolute;right:0px; width:32px;border-left:1px solid #e2e2e2;text-align:center;font-size:12px;color:#888}
        }
      }
    }

    .filter-btn{
      text-align: right;;
      margin:20px 0 30px 0;

      .v-btn{
        background:#292929;
        border:0px;
        color:#fff;
      }
    }

  }

  
  .footer-btns{
    text-align:right;
    padding:20px;
    font-family:'SCDream';

    .v-btn{
      margin-left:10px;
      border:1px solid #c2c2c2;
      letter-spacing: 0px;
      font-weight:500;
    }
    .v-btn.ok{
      border:1px solid #EE2073;
      color:#EE2073;     
    }
  }
}

.message-cont{
  font-family:'SCDream';
  dt{
    strong{font-size:20px;color:#494949;font-weight:500}
  }
  dd{
    strong{font-size:20px;color:#EE2073;font-weight:500}
  }
}

</style>