<template>
  <div>
    <button class="btn btn-default" @click="toAddLinkman">添加联系人</button><br />

    <table class="table table-hover">
            <thead>
              <tr>
                <th>联系人编号</th>
                <th>联系人名字</th>
                <th>联系人邮箱</th>
                <th>联系人电话</th>
                <th>联系人qq</th>
                <th>所属人</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="linkman in linkmans">
                <td>{{linkman.id}}</td>
                <td>{{linkman.name}}</td>
                <td>{{linkman.email}}</td>
                <td>{{linkman.phone}}</td>
                <td>{{linkman.qq}}</td>
                <td>{{linkman.user.username}}</td>
              </tr>
            </tbody>
          </table>
  </div>
</template>

<script>
  export default{
    data:function(){
      return {
        linkmans:[],
      }
    },

    mounted:function(){
      this.getLinkmans();
    },
    methods:{
      toAddLinkman:function(){
        this.$router.push("/main/addLinkman");
      },
      getLinkmans:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/linkmanController/getLinkmans",
          data:{time:new Date().getTime()},
          success:function(result){
              if(result.code == "200"){
                obj.linkmans =  result.data;
              }else{
                alert("有问题，请联系管理员");
              }
          },
          xhrFields: {
            withCredentials: true
          }
        });



      }

    }


  }
</script>

<style>
</style>
