<template>
  <v-dialog 
    persistent
    v-model="state"
    width="300px"
  >
    <div class="progress">
      <v-progress-circular
      :size="40"
      width="5"
      color="#D20A61"
      indeterminate
      ></v-progress-circular>
      <div class="progress-text">
        장비에 금액을 <strong>투입중</strong>입니다
      </div>
      <p>잠시만 기다려주세요</p>
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

.progress{
  background:#fff;
  padding:30px;
  display:flex;
  flex-direction: column;
  align-items:center;
  justify-content: center;

  .progress-text{
    margin-top:20px;
    font-family:'SCDream';
    strong{
      color:#D20A61;
      font-weight:500
    }
  }

  p{
    font-family: 'SCDream';
    font-size:12px;
    margin-top:5px;
    color:#888;
    margin-bottom:0px;
  }
}

</style>