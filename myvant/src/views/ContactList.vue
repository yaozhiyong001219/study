<template>
  <div class="home">
   <!-- 联系人列表 -->
<!-- 联系人列表 -->
<van-popup v-model="showList" position="bottom">
  <van-contact-list
    :list="list"
    @add="onAdd"
    @edit="onEdit"
  />
</van-popup>
<!-- 联系人编辑 -->
<van-popup v-model="showEdit" position="bottom">
  <van-contact-edit
    :contact-info="editingContact"
    :is-edit="isEdit"
    @save="onSave"
    @delete="onDelete"
  />
</van-popup>


  </div>
</template>

<script>
// @ is an alias to /src

import {  Button   } from 'vant';
import {  ContactList,Toast,ContactEdit,Popup } from 'vant';
import axios from 'axios'

export default {
  name: "ContactList",
  components: {
    [ContactList.name]: ContactList,
    [ContactEdit.name]: ContactEdit,
    [Popup.name]: Popup,
  },
   data(){
    return {
      showList: true,
      showEdit: false,
      isEdit: false,
      list: [],
      instance:null , //axios 实例
      editingContact:{}
    }
  },
  methods:{
    //获取联系人列表
    getList()
    {
      this.instance.get('contactlist').then(res=>{
      
      this.list=res.data.data
    }).catch(err=>{
      console.log(err),
      Toast('请求失败')
    })

    },
    //增加联系人
   onAdd() {
      this.editingContact = { id: this.list.length };
      this.isEdit = false;
      this.showEdit = true;
    },

    // 编辑联系人
    onEdit(item) {
      this.isEdit = true;
      this.showEdit = true;
      this.editingContact = item;
    },

    onSave(item){
      if(this.isEdit)
      {
        //编辑保存
         this.instance.put('/contact/edit',item).then(res=>{
          if(res.data.code=200)
          {
          Toast('编辑成功')
          this.getList()
          this.showEdit=false
          }
          
        }).catch(()=>{
           Toast('请求失败')
        })
      
      }else{
        //新建保存

        this.instance.post('/contact/new/json',item).then(res=>{
          if(res.data.code=200)
          {
          Toast('新建成功')
          this.getList()
          this.showEdit=false
          }
          
        }).catch(()=>{
           Toast('请求失败')
        })
      }
      
    },

    onDelete(item){
      this.instance.delete('/contact',{
        params:{
          id:item.id
        }
      }).then(res=>{
        if(res.data.code=200){
          Toast('删除成功')
          this.showEdit=false
          this.getList()

        }else
        {
           Toast('请求失败')
        }
      })

    },

  },
 
  created(){

    this.instance=axios.create({
      baseURL:'http://localhost:9000/api',
      timeout:1000
    })

   this.getList();

  }
}
</script>
<style scoped>
  .van-contact-list{
    z-index: 0;
    
  }
  .van-Popup{
    height: 100%;
  }
</style>
