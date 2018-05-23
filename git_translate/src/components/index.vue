<template>
    <!-- <h1>Index</h1> -->
    <div id="translate">
      <form >
        <input type="text" v-model="iptCont">
        <select name="lan" v-model="language">
          <option  v-for="(value,key,index) in lanOpts" :value="key">{{ value }}</option>
        </select>
        <input @click="contSub" type="submit" value="提交" />
      </form>

    </div>
</template>

<script>
export default {
  name: 'Index',
  data () {
    return {
      iptCont:'',
      lanOpts:{
        en:'English',
        zh:'Chinese',
        ko:'Korean'
      },
      language:'English'
    }
  },
  created:function(){
    // console.log(this.lanOpts);
  },
  methods:{
    contSub (e) {
      //取消默认事件,防止提交表单自动刷新
      e.preventDefault();
      // console.log(this.iptCont);
      // console.log('我是子组件index:' + this.iptCont);
      
      //业务逻辑:需要将index获取的输入内容返回给app.vue,利用vue 的 $emit。
      //1、父组件可以使用 props 把数据传给子组件。

      //2、子组件可以使用 $emit 触发父组件的自定义事件
            // 子组件通过emit定义的事件,在父引入自组件的时候可以绑定该定义事件,并绑定为自己的事件(自命名),绑定的事件可以附带数据
      this.$emit('emitContSub',this.iptCont,this.language);
      // console.log(this.language); 表单提交后
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
