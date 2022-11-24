<template>
  <!----Start container-------------------->
  <div class="container">

    <!---Start desk----------------------->
      <div class="desk">
        <!----Start Box 1 ------------------>
        <div class="box" id="box_1">
          <img class="image" :src="require(`./assets/${fruits[firstBox-1].image}`)" />
        </div>
        <!----End Box 1 ------------------>
        <!----Start Box 2 ------------------>
        <div class="box" id="box_2">
          <img class="image" :src="require(`./assets/${fruits[secondBox-1].image}`)" />
        </div>
        <!----End Box 2 ------------------>
        <!----Start Box 3 ------------------>
        <div class="box" id="box_3">
          <img class="image" :src="require(`./assets/${fruits[thirdBox-1].image}`)" />
        </div>
        <!----End Box 3 ------------------>
        <!----Start score ------------------>
        <div class="score">امتیاز شما : {{score}}</div>
        <!---------End score--------------->
        <!----Start begin button ------------------>
        <div class="button" @click="start()">شروع</div>
        <!----End  begin button ------------------>
        <!----Start cash out button ------------------>
        <button class="cash_out" id="cash" :disabled="cash_out_disable" @click="cash_out()">نقد کردن</button> 
         <!----End cash out button ------------------>    
      </div>
      <!----End desk-------------------->
  </div>
  <!----End container-------------------->
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      score : 10,
      firstBox : null,
      setIntevalFirstBox : null,
      secondBox : null,
      setIntervalSecondBox : null,
      thirdBox : null,
      setIntervalThirddBox : null,
      cash_out_disable : false,
      fruits : [
        {key : "cheey" , image : "1.jpg" },
        {key : "lemon" , image : "2.jpg" },
        {key : "orange" , image : "3.png" },
        {key : "watermelon" , image : "4.jpg" }
      ]
    }
  },
  methods : {
    // --------------Start defaultState method ----------------------//
    // زمانیکه کامپوننت ساخته می شود فراخوانی می شود و سه عکس تصادفی در باکس ها قرار می گیرند //
    defaultState()
    {
      this.firstBox = Math.floor(Math.random() * 4) + 1;
      this.secondBox = Math.floor(Math.random() * 4) + 1;
      this.thirdBox = Math.floor(Math.random() * 4) + 1;
    },
    //----------End defaultState method ----------------------------//
    //----------Start operateStart method---------------------------------//
    // زمانیکه متود استارت فاراخوانی می شود برای جلوگیری از تکرار کد است تا سه با فراخوانی نشود
    operateStart(state_1,state_2,state_3){
      let counter_1 = 0;
      let counter_2 = 0;
      let counter_3 = 0;
      this.setIntevalFirstBox = setInterval(()=>{
          this.firstBox =  Math.floor(Math.random() * 4) + 1;
          counter_1++;
          if(counter_1==20)
          {
            this.firstBox = state_1;
            document.getElementById('box_1').classList.remove('turn');
            clearInterval(this.setIntevalFirstBox)
          }
        },150);

        this.setIntervalSecondBox =  setInterval(()=>{
          this.secondBox =  Math.floor(Math.random() * 4) + 1;
          counter_2++;
          if(counter_2==27)
          {
            this.secondBox = state_2;
            document.getElementById('box_2').classList.remove('turn');
            clearInterval(this.setIntervalSecondBox)
          }
        },150);
        this.setIntervalThirddBox =  setInterval(()=>{
          this.thirdBox =  Math.floor(Math.random() * 4) + 1;
          counter_3++;
          if(counter_3==35)
          {
            this.thirdBox = state_3;
            document.getElementById('box_3').classList.remove('turn');
            clearInterval(this.setIntervalThirddBox)
            if(state_1 == state_2 && state_2 == state_3)
            {
              if(state_1 == 1)
              this.score+=10;
              else if(state_1 == 2)
              this.score+=20;
              else if(state_1==3)
              this.score +=30;
              else if (state_1 == 4)
              this.score += 40;
            }
          }
        },150);
    },
    //---------End operateStart method-------------------------------------//
    //------------Start start method--------------------------------------//
    // وقتی روی دکمه شروع کلیک کنم این متود فراخوانی می شود
    start()
    {
      this.score--;
      const state_1 = Math.floor(Math.random() * 4) + 1;
      const state_2 = Math.floor(Math.random() * 4) + 1;
      const state_3 = Math.floor(Math.random() * 4) + 1;

      document.getElementById('box_1').classList.add('turn');
      document.getElementById('box_2').classList.add('turn');
      document.getElementById('box_3').classList.add('turn');
      
      console.log(state_1,state_2,state_3)
      if(this.score<40)
      this,this.operateStart(state_1,state_2,state_3)
      
      else if (this.score >= 40 && this.score<=60)
      {
        while(true)
        {
          if(state_1 == state_2 && state_2 == state_3)
          {
            const chance =  Math.floor(Math.random() * 100) + 1;
            if(chance >=1 && chance <=30)
            break;
            else if (chance >=31 && chance <=100)
            {
              state_1 = Math.floor(Math.random() * 4) + 1;
              state_2 = Math.floor(Math.random() * 4) + 1;
              state_3 = Math.floor(Math.random() * 4) + 1;
            }
          }
          else
          break;
        }
        this.operateStart(state_1,state_2,state_3);
      }
      else if( this.score >= 60)
      {
        while(true)
        {
          if(state_1 == state_2 && state_2 == state_3)
          {
            const chance =  Math.floor(Math.random() * 100) + 1;
            if(chance >=1 && chance <=60)
            break;
            else if (chance >=61 && chance <=100)
            {
              state_1 = Math.floor(Math.random() * 4) + 1;
              state_2 = Math.floor(Math.random() * 4) + 1;
              state_3 = Math.floor(Math.random() * 4) + 1;
            }
          }
          else
          break;
        }
        this.operateStart(state_1,state_2,state_3);
      }
    },
    //--------------End start method--------------------------------------//
    //--------Start cash out method--------------------------------------//
    cash_out()
    {
      const chance =  Math.floor(Math.random() * 100) + 1;
      if(chance>=1 && chance <=50)
      {
        const degree =  Math.floor(Math.random() * 360);
          const sin = Math.sin(degree* Math.PI / 180)
          const cos = Math.cos(degree* Math.PI / 180)
          console.log(Math.floor(cos*300) , Math.floor(sin*300))
          document.getElementById('cash').style.bottom = 100 + 
          console.log(document.getElementById('cash').offsetLeft)
          document.getElementById('cash').style.left = (document.getElementById('cash').offsetLeft) + (Math.floor(cos*300)) + 'px'
          document.getElementById('cash').style.top = (document.getElementById('cash').offsetTop) + (Math.floor(sin*300)) + 'px'
          if(document.getElementById('cash').offsetLeft<0)
          document.getElementById('cash').style.left = 0 + 'px'
          if(document.getElementById('cash').offsetTop>=800 || document.getElementById('cash').offsetTop<0 )
          document.getElementById('cash').style.top = 0 + 'px'
      }
      else if(chance>50&&chance<=90)
      this.cash_out_disable = true
    }
    //-----------End cash out methos ---------------------------------------//
  },
  created()
  {
    this.defaultState()
  },
  mounted()
  {
    document.getElementById('cash').style.to = 780 + 'px'
    document.getElementById('cash').style.left = 20 + 'px'
  }
}
</script>

<style>
/*------Start container-----------------*/
.container
{
  width : 100%;
  height : 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position : relative;
}
/*------Start desk----------------------------- */
.desk
{
  width : 80%;
  height : 80vh;
  background: #8B4513;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  gap : 30px ; 
  outline: 10px solid 	#D2691E;
}
/*-----Start score-------------*/
.score
{
  position: absolute;
  top : 20px;
  right : 30px;
}
/*-----End Score---------------*/
/*---------Start box-------------*/
.box
{
  width : 250px;
  height : 250px;
  position: relative;
  border: 5px solid #d35400;
  transform: translateY(-20px);
  background: #fff;
 
}
/*------Start image------------*/
.image
{
  width : 100%;
  height: 100%;
}
/*---------End image------------*/
/*---------End box---------------*/
.button
{
  font-size: 25px;
  padding : 10px 20px;
  background: #2980b9;
  color : #fff;
  position: absolute;
  right : 20px;
  bottom: 20px;
  border-radius : 10px ;
  cursor: pointer;
}
.turn
{
  animation : example 0.5s infinite;
}
@keyframes example {
  0%   {transform: rotateY(0deg);}
  50%  {transform: rotateY(180deg);}
  100% {transform: rotateY(0deg);}
}
/*----------Start cash out-----------*/
.cash_out
{
  font-size: 25px;
  width : 120px;
  height : 75px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #2980b9;
  color : #fff;
  position: absolute;
  left : 20px;
  bottom: 20px;
  border-radius : 10px ;
  cursor: pointer;
  z-index: 20;
}
/*----------End cash out-----------*/
/*--------End desk-------------------*/
/*------End container-----------------*/
</style>
