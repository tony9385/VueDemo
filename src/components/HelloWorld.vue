<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
  <button v-on:click="counter += 1">增加 1</button>
  <p>这个按钮被点击了 {{ counter }} 次。</p>
<!-- <ve-histogram :data="chartData"></ve-histogram> -->
<img :src="bar1">
   <button v-on:click="greet">Greet</button>
   <button v-on:click="bar('1')">bar1</button>
   <button v-on:click="bar('2')">bar2</button>
   <button v-on:click="startCallAPI">Start</button>
   <button v-on:click="stopCallAPI">Stop</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
       counter: 0,
       chatTimer:null,
       bar1:"",
       bar2:"",
       chartData: {
        columns: ['日期', '访问用户', '下单用户', '下单率'],
        rows: [
          { '日期': '2020-1-11', '访问用户': 1393, '下单用户': 1093, '下单率': 0.32 },
          { '日期': '2020-2-2', '访问用户': 3530, '下单用户': 3230, '下单率': 0.26 },
          { '日期': '1/3', '访问用户': 2923, '下单用户': 2623, '下单率': 0.76 },
          { '日期': '1/4', '访问用户': 1723, '下单用户': 1423, '下单率': 0.49 },
          { '日期': '1/5', '访问用户': 3792, '下单用户': 3492, '下单率': 0.323 },
          { '日期': '1/6', '访问用户': 4593, '下单用户': 4293, '下单率': 0.78 }
        ]
      }
    }
  },
  methods: {  
 greet: function (event) {
      // `this` 在方法里指当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
          alert(event.target.tagName)
      }
    }    ,
    bar:function(arg){
      console.log(arg);
      console.log("bar");
        this.bar1='../static/img/bar'+arg+'.png';
        console.log(this.bar1)
    }
    ,
    startCallAPI:function(event){
      console.log('start');
       this.chatTimer= setInterval(this.callAPI,1000);
    },
    callAPI:function(){
      console.log('a');
      if(this.bar1=="../static/img/bar1.png")
      {
         this.bar1='../static/img/bar2.png';
      }
      else
      {
        this.bar1='../static/img/bar1.png';
      }
      axios.post("http://www.runoob.com/try/ajax/demo_test_post.php",{
			name:"菜鸟教程",
			url:"http://www.runoob.com"
    })
    .then(function (response){ console.log(response);})
    .catch(function (error){console.log(error);})
      
    },
    stopCallAPI:function(){
      console.log('stop');
      clearInterval(this.chatTimer);
      this.chatTimer=null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
