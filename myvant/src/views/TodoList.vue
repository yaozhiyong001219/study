<template>

<div class="root">
    <input v-model="inputValue" />
    <button @click="sclick">提交</button>
    <br>
    <!-- <ul>     
        <li v-for="(item,index) in mylist" :key="index">{{item}}{{index}}</li>
    </ul> -->
    <TodoItem  v-for="(item,index) of mylist" :key="index"
        :content=item
        :index=index
        @delete="sDelete" 
     >
    </TodoItem>
</div>
</template>
<script>
import TodoItem from '../components/TodoItem'
export default {
    name:'TodoList',
    components:{
        TodoItem
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
           this.inputValue=''
       },
       sDelete:function(index){
           this.mylist.splice(index,1)
       }
    }
   
}
</script>

<style>
ul{
    width: 100px;
}
</style>