<template>
  <div id="app">
    <input v-model="message"><!--下方语句的简写，语法糖-->
    <input :value="message" @input="handleChange">
    {{message}} {{message + message}}<!--可以支持表达式，但不支持语句-->
        <div :id = "message"></div><!--将id名字与message绑定一起，用v-bind：或者直接简写成：-->
        <todo-list><!--如果如下用index作为索引，key的index为0就会有问题-->
            <todo-item @delete="handleDelete" v-for="(item, index) in list" :key="index" :title="item.title" :del="item.del">
                <template v-slot:pre-icon="{value}"><!--新语法：具名插槽-->
                    <span>前置图标{{value}}</span>
                </template>
                <template v-slot:suf-icon>
                    <span>后置图标</span>
                </template>
                <!--<span slot="pre-icon">前置图标</span>老语法
                <span slot="suf-icon">后置图标</span>-->
            </todo-item>
        </todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import TodoItem from './components/TodoItem.vue'

export default {
  name: 'app',
  components: {
    TodoList,
    TodoItem
  },
  data(){
    return {
      message: 'Hello World',
      list:[{
          title: '课程1',
          del: true
      }, {
          title: '课程2',
          del: false
      }],
    }
  },
  methods: {
    handleChange(e) {
      this.message = e.target.value
    },
    handleDelete(val){//var就是把this.title传给它
        console.log('handleDelete', val)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
