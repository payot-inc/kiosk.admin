<template>
  <div class="member-list">
    <OptionBox/>
    <DataTable :data="data" paging="true">
      <template slot="table-top-btns">
        <div class="btns">
          <v-btn outlined class="exel">
            <v-icon>mdi-microsoft-excel</v-icon>
            <label>엑셀출력</label>
          </v-btn>
          <v-btn outlined class="point-all" @click="$refs.pointAll.open(true)">
            <v-icon>mdi-alpha-p-circle</v-icon>
            <label>포인트 일괄지급</label>
          </v-btn>
        </div>
      </template>
      <template slot="data-useButton" slot-scope="{ data }">
        <v-btn outlined @click="$refs.userInfo.open(true)">이용내역 보기</v-btn>
        <v-btn outlined @click="$refs.pointModal.open(true)">포인트 지급/차감</v-btn>
      </template>
    </DataTable>

    <UserInfo ref="userInfo"/>
    <PointModal ref="pointModal"/>
    <PointAll ref="pointAll" />
  </div>
</template>

<script>
import PointModal from '@/components/modal/point.vue';
import DataTable from '@/components/data-table.vue';
import OptionBox from '@/components/optionBox.vue';
import UserInfo from '@/components/modal/user-info.vue';
import PointAll from '@/components/modal/point-all.vue';

export default {
  components:{
    DataTable, OptionBox, UserInfo, PointModal,PointAll
  },

  data(){
    return{
      toggle:'no',
      data:{
        thead:[
            { label: '회원번호', value: 'memberNumber' },
            { label: '가입날짜', value: 'date' },
            { label: '총 결제금액', value:'totalPrice'},
            { label: '총 충전포인트', value:'totalPoint'},
            { label: '총 보너스포인트', value: 'bonusPoint'},
            { label: '총 차감포인트', value:'minusPoint'},
            { label: '남은 포인트', value: 'userPoint' },
            { label: '버튼', value: 'useButton' },
          ],
        tbody:[
          {
            memberNumber:'010-8525-4561',
            date:'2020-02-14',
            totalPrice:34500+'원',
            totalPoint:34500+'P',
            bonusPoint:500+'P',
            minusPoint:4500+'P',
            userPoint:850+'P',
            buttons: null,
          },
          {
            checkbox:null,
            memberNumber:'010-8525-4561',
            date:'2020-02-14',
            totalPrice:34500+'원',
            totalPoint:34500+'P',
            bonusPoint:500+'P',
            minusPoint:4500+'P',
            userPoint:850+'P',
            buttons: null,
          },

        ]
      }
    }
  },
  
}
</script>


<style lang="scss" scoped>

.btns{

  .v-btn{
      height:32px;
      border-radius:5px;
      margin-left:10px;
      .v-icon{font-size:22px;}
      label{letter-spacing:0px;margin-left:10px;}
  }

  .v-btn.exel{
    border:1px solid #139B3B;
    .v-icon{color:#139B3B}
    label{color:#139B3B}
  }

  .v-btn.point-all{
    border:1px solid #EE2073;
    .v-icon{color:#EE2073}
    label{color:#EE2073}
  }
}
  
</style>