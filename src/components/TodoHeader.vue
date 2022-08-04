<template>
  <header class="header">
    <h1>todos</h1>
      <!--这个checkbox是隐藏的-->
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll"> 
       <!--通过label来控制checkbox的选择 , 也就是这个下箭头-->
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model="task"
      @keydown.enter="downFn"
    />
  </header>
</template>

<script>
export default {
  props:['harr'],
  data(){
    return{
      task: ''
    }
  },
  methods:{
    downFn(){
      if(this.task.trim().length === 0) return alert('不能为空')
      this.$emit('create', this.task)
      this.task = ''
    }
  },
  //全选
  computed:{
    isAll:{
      set(checked){
        this.harr.forEach(item=>item.isDone = checked)
      },
      get(){
        return this.harr.length > 0 && this.harr.every(item=>item.isDone === true)
      }
    }
  }
}
</script>