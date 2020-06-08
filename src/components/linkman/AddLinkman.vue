<template>
  <div>
     联系人姓名:<input type="text" v-model="name"/><br />
     联系人电话:<input type="text" v-model="phone"/><br />
     联系人邮箱:<input type="text" v-model="email"/><br />
     联系人qq:<input type="text" v-model="qq"/><br />
     <button class="btn btn-default" @click="addLinkman">添加</button>
  </div>
</template>
<script>
  export default{
    data:function(){
      return {
          name:"",
          phone:"",
          email:"",
          qq:"",
          userId:0
      }
    },
     mounted:function(){
       this.getUser();
     },
    methods:{
      addLinkman:function(){
        var obj = this;
        $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/linkmanController/addLinkman",
            data:{time:new Date().getTime(),name:obj.name,phone:obj.phone,email:obj.email,qq:obj.qq,userId:obj.userId},
            success:function(result){
              if(result.code == "200"){
                alert("添加成功");
              }else{
                alert("添加失败");
              }
            },
            xhrFields: {
              withCredentials: true
            }
          });
      },


     getUser:function(){
       var obj = this;
       $.ajax({
           type:"post",
           url:"http://localhost:8082/crm/userController/user",
           data:{time:new Date().getTime()},
           success:function(result){
               if(result.code == "200"){
                 obj.userId = result.user.id;
               }else{
                 obj.$router.push("/");
               }
           },
           xhrFields: {
             withCredentials: true
           }
         });
     },

    }



  }
</script>

<style>
</style>
