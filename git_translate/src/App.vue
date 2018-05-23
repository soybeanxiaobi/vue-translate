<template>
  <div id="app">
    <h1>在线翻译</h1>
    <h5>简单 / 易用 / 便捷</h5>
    <!-- <img src="./assets/logo.png"> -->
    <!-- <HelloWorld/> -->
    <index v-on:emitContSub="emitParentContSub"/>
    <div id="showCont">
      <!-- <span>{{ translateCont }}</span> -->
      <translateTextVue v-text="translateCont" />
    </div>
  </div>
</template>

<script>
import index from './components/index'
import translateTextVue from './components/translateText'


export default {
  name: 'App',
  components: {
      index:index,
      translateTextVue:translateTextVue,
  },
  data(){
    return {
      translateCont:'',

    }
  },
  methods:{
    emitParentContSub(data,language){
        // console.log('我是父组件App:' + data);
        //调用翻译API
        this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180509T123813Z.bb69429520db94b9.d161c9797080434daafab03aafb91fa71342a340&lang='+ language +'&text=' + data)
        .then((req) => {

            console.log(req);
            this.translateCont = req.body.text[0];
        })
    }
  }
}
</script>

<style>
#app{
  text-align: center;
}
h5{
  color:#ccc;
}
</style>
