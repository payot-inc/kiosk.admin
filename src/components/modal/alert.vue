<template>
  <v-dialog
    v-model="state"
    width="420px"
  >
    <div class="alert-modal">
      <div class="modalTitle">
        <h4><span>선택한 상품은 없는 상품입니다</span></h4>
        <p>다시 한번 확인해주세요</p>
      </div>

      <div class="btns">
        <v-btn outlined class="ok" @click="open(false)">
          확인
        </v-btn>
      </div>
    </div>
  </v-dialog>
</template>

<script>
export default {
  data(){
    return{
      state:true,
      number:0,
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

.alert-modal{
  background:#fff;
  padding:20px;

  .modalTitle{
    border-bottom:1px dashed #e2e2e2;
    margin-bottom:20px;
    text-align:center;

    h4{
      font-size:20px;font-family:'SCDream';font-weight:500;
      span{color:#EE2073;}
    }
    p{margin-top:5px;font-size:14px;color:#888}
  }


  .btns{
    text-align:center;

    .v-btn{
      margin-left:10px;
      border:1px solid #c2c2c2;
      letter-spacing: 0px;
    }
    .v-btn.ok{
      border:1px solid #EE2073;
      color:#EE2073
    }
  }
}

</style>