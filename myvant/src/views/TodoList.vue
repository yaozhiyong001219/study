<template>

<div class="root">
    <input v-model="inputValue" />
    <button @click="sclick">提交</button>
    <br>
    <ul>     
        <li v-for="(item,index) in mylist" :key="index">{{item}}{{index}}</li>
    </ul>
</div>
</template>
<script>
export default {
    name:'TodoList',
    components:{

    },
    data(){
        return {
        inputValue:'hello',
        mylist:[1,2,3,4,5,6]
        }
        
    },
    methods:{
       sclick: function(){
           this.mylist.push(this.inputValue)
       }
    }
   
}
</script>

<style>
ul{
    width: 100px;
}
</style>