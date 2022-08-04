<template>
  <div class="todoapp">
    <TodoHeader :harr="list" @create="createFn"></TodoHeader>
    <TodoMain :arr="showArr" @del="delFn"></TodoMain>
    <TodoFooter :farr="showArr" @change="changeFn" @clear="clearFn"></TodoFooter>
  </div>
</template>

<script>
//css 样式引入
import "./styles/base.css";
import "./styles/index.css";
//组件引入
import TodoHeader from "./components/TodoHeader.vue";
import TodoMain from "./components/TodoMain.vue";
import TodoFooter from "./components/TodoFooter.vue";
export default {
  //组件注册
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem('todoList')) || [],
      getSel: "all",
    };
  },
  methods: {
    //新增功能
    createFn(taskname) {
      let id =
        this.list.length == 0 ? 100 : this.list[this.list.length - 1].id + 1;
      this.list.push({
        id,
        name: taskname,
        isDone: false,
      });
    },
    //删除功能
    delFn(id) {
      let index = this.list.findIndex((item) => (item.id = id));
      this.list.splice(index, 1);
    },
    //数据切换
    changeFn(str) {
      this.getSel = str;
    },
    //清除已完成
    clearFn(){
      this.list = this.list.filter(item=>item.isDone === false)
    }
  },
  computed: {
    //数据切换功能实现
    showArr() {
      if ((this.getSel === "yes")) {
        return this.list.filter(item => item.isDone === true);
      } else if ((this.getSel === "no")) {
        return this.list.filter(item => item.isDone === false);
      } else {
        return this.list;
      }
    },
  },
  watch:{
    list:{
      deep: true,
      handler(){
        localStorage.setItem('todoList', JSON.stringify(this.list))
      }
    }
  }
};
</script>

<style></style>
