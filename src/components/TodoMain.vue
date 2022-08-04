<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{completed: item.isDone}" v-for="item in arr" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone"/>
        <label>{{item.name}}</label>
           <!--鼠标悬浮之后显示的x , 删除任务按钮-->
        <button class="destroy" @click="deleteFn(item.id)"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
export default {
  props:['arr'],
  methods:{
    deleteFn(id){
      this.$emit('del', id)
    }
  }
}
</script>