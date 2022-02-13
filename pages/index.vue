<template>
  <div class="container">
    <div class="input">
      <div class="result"> {{result}} </div>
      <input type="text" v-model="text">
    </div>
    <div class="buttons">
      <a class="btn c-btn" @click="cBtn">C</a>
      <a class="btn alternate-func-btn" @click="funcBtn('(')">(</a>
      <a class="btn alternate-func-btn" @click="funcBtn(')')">)</a>
      <a class="btn func-btn" @click="funcBtn('*')">X</a>
      <a class="btn alternate-func-btn" @click="funcBtn('√')">√</a>
      <a class="btn alternate-func-btn" @click="funcBtn('%')">%</a>
      <a class="btn alternate-func-btn" @click="funcBtn('!')">
        <span>+</span>
        <span>-</span>
      </a>
      <a class="btn func-btn" @click="funcBtn('/')">/</a>
      <a class="btn default-btn" @click="numberBtn(7)">7</a>
      <a class="btn default-btn" @click="numberBtn(8)">8</a>
      <a class="btn default-btn" @click="numberBtn(9)">9</a>
      <a class="btn func-btn" @click="funcBtn('-')">-</a>
      <a class="btn default-btn" @click="numberBtn(4)">4</a>
      <a class="btn default-btn" @click="numberBtn(5)">5</a>
      <a class="btn default-btn" @click="numberBtn(6)">6</a>
      <a class="btn func-btn" @click="funcBtn('+')">+</a>
      <a class="btn default-btn" @click="numberBtn(1)">1</a>
      <a class="btn default-btn" @click="numberBtn(2)">2</a>
      <a class="btn default-btn" @click="numberBtn(3)">3</a>
      <a class="btn func-btn" @click="resultFunc()">=</a>
      <a class="btn default-btn" @click="numberBtn('.')">.</a>
      <a class="btn default-btn" @click="numberBtn(0)">0</a>
      <a class="btn default-btn" @click="removeLastChar">⟵</a>
      <a href="mailto:ecakmak91@gmail.com" class="btn func-btn">Me</a>
    </div>
  </div>
</template>

<script>
import { create, all } from 'mathjs'

const config = { }
const math = create(all, config)



export default {
  data(){
    return{
      result:0,
      text:0,
      value1:0,
      value2:0,
      isResult:false,
      opr:0,
    }
  },
  methods:{
    numberBtn(data){
      if(this.text!==0)
        this.text+=""+data
      else
        if(data!==".")
          this.text=data
        else
          this.text="0."
      
      //this.resultFunc()
    },
    cBtn(){
      this.text=0;
      this.result=0;
      this.value1=0;
      this.value2=0;
    },
    funcBtn(funcName){
      let lastChar=this.text.slice(-1)
      
      if(!Number.isInteger(parseInt(lastChar))){
        this.text = this.text.slice(0, -1);
      }

      if(this.text!==0){
        this.text+=funcName;
        this.lastSign=funcName
        
      }else{

        this.text=funcName;
      }
      
    },
    resultFunc(){
      this.result=math.evaluate(this.text)
    },
    removeLastChar(){
      this.text = this.text.slice(0, -1); 
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
a{
  cursor:pointer;
  text-decoration: none;
  color:inherit;
}
.container .input{
  width: 210px;
  background: #fff;
}
.container .input input{
  width: 100%;
  padding: 5px 10px;
  border:none;
  text-align: right;
  font-size: 30px;
  
}
.container .input .result{
  width: 100%;
  padding: 5px 10px;
  border:none;
  text-align: right;
  font-size: 18px;
}
.container .buttons{
  width: 210px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  
}
.container .buttons a.btn{
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #edf2f5;
  border-radius: 5px;
  margin: 5px;
}
.container .buttons a.btn.c-btn{
  background:#e94333;
  color:#fff;
}
.container .buttons .alternate-func-btn{
  color:#e94333;
}
.container .buttons .func-btn{
  color:#4358e8;
}



</style>
