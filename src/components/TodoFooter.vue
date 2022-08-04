<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{count}}</strong></span>
    <ul class="filters" @click="fn">
      <li>
        <a :class="{selected: isSel === 'all'}" href="javascript:;" @click="isSel = 'all'">全部</a>
      </li>
      <li>
        <a :class="{selected: isSel === 'no'}" href="javascript:;" @click="isSel = 'no'">未完成</a>
      </li>
      <li>
        <a :class="{selected: isSel === 'yes'}" href="javascript:;" @click="isSel = 'yes'">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="clearbtn">清除已完成</button>
  </footer>
</template>

<script>

export default {
  props:['farr'],
  data(){
    return{
      isSel: 'all'
    }
  },
  computed:{
    count(){
      return this.farr.length
    }
  },
  methods:{
    fn(){
      this.$emit('change', this.isSel)
    },
    clearbtn(){
      this.$emit('clear')
    }
  }
}
</script>