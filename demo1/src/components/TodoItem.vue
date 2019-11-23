<template>
    <li>
        <slot name="pre-icon" :value="value"></slot>
        <span class="red" v-if="!del">{{title}}</span>
        <span v-else style="text-decoration: line-through;">{{title}}</span>
        <slot name="suf-icon">hhh</slot>
        <button v-show="!del" @click="handleClick">删除</button>
    </li>
</template>
<script>
export default {
    props:{
        title: String,
        del:{
            type: Boolean,
            default: false,
            },
    },
    data: function (){
        return {
            value: Math.random()//使用todoitem的时候，我们想要拿到里面的value值，我们想根据value的不同给它传递相应的内容（template）
        }
    },
    methods: {
        handleClick(){
            console.log('点击删除按钮')
            this.$emit('delete',this.title)//抛出参数，todoitem标签需要参数和方法。第一个参数是与todoitem标签的delete方法绑定，第二个参数是接收这个方法的参数
        }
    },
}
</script>
<style scoped>
.red {
    color:red;
}
</style>