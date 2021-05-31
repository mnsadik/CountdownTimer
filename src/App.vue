<template>
  <div class="container">
    <h1 class="text-center">Countdown Timer</h1>
    <DisplayTime :year="receivedYear" :month="receivedMonth" :date="receivedDate" :hour="receivedHour" :minute="receivedMinute" :clockState="startClock"/> <!-- v-on:emitMonth="emitedMonth()" -->
    <GetTime v-on:catchit="gotit($event)" v-if="clockWidge"/>
    <div class="row justify-content-md-center btnWidge" v-if="btnWidge">
      <!-- <div class="col-sm-2"><button class="btn btn-primary" style="width:100%" @click="pausebtn()">{{pauseBtnTxt}}</button></div> -->
      <div class="col-sm-2"><button class="btn btn-primary" style="width:100%" onClick="window.location.reload()">Reset</button></div>
    </div>
  </div>
</template>

<script>

import GetTime from './components/get_time.vue';
import DisplayTime from './components/display_time.vue'

export default {
  name: 'App',
  components: {
    GetTime, //Components key
    DisplayTime, //Components key
  },
  data(){
    return{
      receivedYear:'',
      receivedMonth:'',
      receivedDate:'',
      receivedHour:'',
      receivedMinute:'',
      startClock: Boolean,

      clockWidge: true,

      btnWidge: false,

      // pauseBtn: Boolean,
      // pauseBtnTxt: 'Pause',
    }
  },
  methods:{
    gotit(pass){
      this.receivedYear= pass.inYears;
      this.receivedMonth= pass.inMonths -1 ;
      this.receivedDate= pass.inDays;
      this.receivedHour= pass.inHours;
      this.receivedMinute= pass.inMinutes;
      this.startClock= pass.setClock;
      this.btnWidge = true;
      this.clockWidge = false;
    },
    // emitedMonth(eMonth){
    //   this.receivedMonth = eMonth;
    // }
    // pausebtn(){
    //   if(this.pauseBtn == false){
    //     this.pauseBtnTxt = 'Pause'
    //     this.pauseBtn = true
    //   }else{
    //     this.pauseBtnTxt = 'Start';
    //     this.pauseBtn = false
    //   }
    //   this.startClock = !this.startClock;
    // }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container,.btnWidge{
  margin: 3em auto;
}
.btnWidge .col-sm-2 .btn{
  margin-bottom: 1em;
}
</style>
