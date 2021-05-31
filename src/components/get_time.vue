<template>
  <div>
    <h4>Set a future Time <span>(Don't set current time)</span> :</h4>
    <form> <!--  @submit.prevent=""-->
      <div class="form-row justify-content-md-center">
        <div class="form-group col-lg-2 col-md-6">
          <input type="number" v-model="handle.inYears" class="form-control" id="yearLabel" name="year" placeholder="Year" @keyup="validYear()">
          <label for="yearLabel">Year {{ invalidYear }}</label>
        </div>
        <div class="form-group col-lg-2 col-md-6">
          <input type="number" v-model="handle.inMonths" class="form-control" id="monthsLabel" name="month" placeholder="Month" @keyup="validMonth()">
          <label for="monthsLabel">Month {{ invalidMonth }}</label>
        </div>
        <div class="form-group col-lg-2 col-md-6">
          <input type="number" v-model="handle.inDays" class="form-control" id="daysLabel" name="date" placeholder="Date" @keyup="validDate()">
          <label for="daysLabel">Date {{ invalidDate }}</label>
        </div>
        <div class="form-group col-lg-2 col-md-6">
          <input type="number" v-model="handle.inHours" class="form-control" id="hoursLabel" name="hour" placeholder="Hour" @keyup="validHour()">
          <label for="hoursLabel">Hour {{ invalidHour }}</label>
        </div>
        <div class="form-group col-lg-2 col-md-6">
          <input type="number" v-model="handle.inMinutes" class="form-control" id="minutesLabel" name="min" placeholder="Minute" @keyup="validMinute()">
          <label for="minutesLabel">Minute {{ invalidMinute }}</label>
        </div>
        <!-- <div class="form-group col-lg-2 col-md-6">
          <input type="number" v-model="inSeconds" class="form-control" id="secondsLabel" name="sec" placeholder="Second" @keyup="validSecond()">
          <label for="secondsLabel">Second {{ invalidSecond }}</label>
        </div> -->
        <div class="form-group col-lg-2 col-md-6">
            <button class="btn btn-primary" style="width:100%" @click="sendit()">Set Time</button>
        </div>
      </div>
    </form>
    
  </div>

</template>

<script>

export default {
    name: 'GetTime',
    data : () => ({

        handle:{
          inYears: new Date().getFullYear(),
          inMonths: new Date().getMonth() + 1,
          inDays: new Date().getDate(),
          inHours: new Date().getHours(),
          inMinutes: new Date().getMinutes(),
          // inSeconds: new Date().getSeconds(),
          setClock: false,
        },

        invalidYear: '',
        invalidMonth: '',
        invalidDate: '',
        invalidHour: '',
        invalidMinute: '',
        // invalidSecond: '',

        curYear: new Date().getFullYear(),
        curMonth: new Date().getMonth() + 1,
        curDate: new Date().getDate(),
        curHour: new Date().getHours(),
        curMinute: new Date().getMinutes(),
    }),

    methods: {

      validYear(){
        if (this.handle.inYears>9999 || this.handle.inYears<this.curYear){
          this.invalidYear = " is invalid";
        }else{
          this.invalidYear = ''
        }
      },
      validMonth(){
        if (this.handle.inMonths>12 || this.handle.inYears==this.curYear && this.handle.inMonths<this.curMonth || this.handle.inMonths<1){
          this.invalidMonth = " is invalid";
        }else{
          this.invalidMonth = '';
        }
      },
      validDate(){
        if (this.handle.inDays>31 || this.handle.inYears==this.curYear && this.handle.inMonths<=this.curMonth && this.handle.inDays<this.curDate || this.inDays<1){
          this.invalidDate = " is invalid"
        }else{
          this.invalidDate = ''
        }
      },
      validHour(){
        if (this.handle.inHours>24 || this.handle.inYears==this.curYear && this.handle.inMonths<=this.curMonth && this.handle.inDays<=this.curDate && this.handle.inHours<this.curHour || this.inHours<0){
          this.invalidHour = " is invalid"
        }else{
          this.invalidHour = ''
        }
      },
      validMinute(){
        if (this.handle.inMinutes>60 || this.handle.inYears==this.curYear && this.handle.inMonths<=this.curMonth && this.handle.inDays<=this.curDate && this.handle.inHours<=this.curHour && this.handle.inMinutes<(this.curMinute + 1) || this.handle.inMinutes<0){
          this.invalidMinute = " is invalid"
        }else{
          this.invalidMinute = ''
        }
      },
      sendit(){
        this.handle.setClock = true;
        this.$emit('catchit', this.handle);
      }
    },
}

</script>

<style scoped>
h4{
    margin: 2em 0 1em 0;
}
span{
  font-weight: 100;
  font-size: 16px;
}
label{
  display: inline-block;
  margin: 10px;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>