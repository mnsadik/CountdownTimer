<template>
    <div class="mainDiv">
        <div class="row justify-content-md-center">
            <!-- <div class="col-lg-1"><h1 id="DisYear">0000</h1><label for="DisYear">Year</label></div>
            <div class="col-lg-1"><h1>:</h1></div>
            <div class="col-lg-1"><h1 id="DisMonth">00</h1><label for="DisMonth">Month</label></div>
            <div class="col-lg-1"><h1>:</h1></div> -->
            <div class="col-sm-1"><h1 id="DisDate">{{displayDays}}</h1><label for="DisDate">Days</label></div>
            <div class="col-sm-1"><h1>:</h1></div>
            <div class="col-sm-1"><h1 id="DisHour">{{displayHours}}</h1><label for="DisHourr">Hours</label></div>
            <div class="col-sm-1"><h1>:</h1></div>
            <div class="col-sm-1"><h1 id="DisMin">{{displayMinutes}}</h1><label for="DisMin">Minutes</label></div>
            <div class="col-sm-1"><h1>:</h1></div>
            <div class="col-sm-1"><h1 id="DisSec">{{displaySeconds}}</h1><label for="DisSec">Seconds</label></div>
        </div>
        <h2 class="text-center endTxt">{{theEnd}}</h2>
    </div>
</template>

<script>

export default {

    name: 'DisplayTime',
    props: ['year', 'month', 'date', 'hour', 'minute', 'clockState'],
    data : () => ({
        displayDays: '00',
        displayHours: '00',
        displayMinutes: '00',
        displaySeconds: '00',

        theEnd: '',
    }),

    computed:{
        _sec: () => 1000,
        _min(){
            return this._sec * 60;
        },
        _hour(){
            return this._min * 60;
        },
        _day(){
            return this._hour * 24;
        },
        end(){
            return new Date(
                this.year,
                this.month,
                this.date,
                this.hour,
                this.minute
            );
        }
    },

    mounted() {
        this.showRemaining();
    },

    methods: {
        showRemaining(){
            const timer = setInterval(()=>{
                if(this.clockState == true){
                    // this.month = this.month -1;
                    const now = new Date();
                    // const end = new Date(2021, 5, 23, 18, 18);
                    const gap = this.end.getTime() - now.getTime();

                    if(gap < 0){
                        this.displayMinutes = '00';
                        this.displaySeconds = '00';
                        this.displayHours = '00';
                        this.displayDays = '00';
                        clearInterval(timer);
                        this.theEnd = 'The End';
                        // window.location.reload();
                        return
                    }

                    const day = Math.floor(gap / this._day);
                    const hour = Math.floor((gap % this._day) / this._hour);
                    const min = Math.floor((gap % this._hour) / this._min);
                    const sec = Math.floor((gap % this._min) / this._sec);
                    this.displayMinutes = min < 10 ? "0" + min : min;
                    this.displaySeconds = sec < 10 ? "0" + sec : sec;
                    this.displayHours = hour < 10 ? "0" + hour : hour;
                    this.displayDays = day < 10 ? "0" + day : day;

                    // this.$emit('emitMonth', this.month);
                }
            }, 1000)  
        }
    },
}
</script>

<style scoped>
.mainDiv{
    margin-top: 3em;
}
.endTxt{
    margin-top: 1em;
}
</style>
