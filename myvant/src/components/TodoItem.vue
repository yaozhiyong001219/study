<template>
<li @click="handleDelete">{{content}}</li>

</template>

<script>
export default {
    props:['content','index'],
    name:'TodoItem',
    methods:{
      handleDelete() {
        // alert(this.index)
        this.$emit("delete",this.index)
      }
    }
}
</script>

<style>

</style>