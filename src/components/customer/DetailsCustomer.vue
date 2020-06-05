<template>
  <div>

    <h2>客户详情</h2>
    客户编号：{{customer.id}}<br />
    客户名字:{{customer.name}}<br />
    客户年龄:{{customer.age}}<br />
    客户性别:{{customer.sex == 0?"男":"女"}}<br />
    客户邮箱:{{customer.email}}<br />
    客户电话:{{customer.phone}}<br />
    客户生日:{{customer.birth}}<br />
    客户级别:{{customer.level == 0 ? "重要客户":(customer.level==1?"普通客户":"潜在客户")}}<br />
    <a href="javascript:void(0)" @click="goback()">返回...</a>

  </div>
</template>

<script>
  export default{
    data:function(){
      return {
        id:this.$route.query.id,
        customer:{}
      }
    },
    mounted:function(){
      this.getCustomer();
    },
    methods:{
      goback:function(){
        this.$router.go(-1)
      }
      ,
      getCustomer:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/customerController/getCustomerById",
          data:{time:new Date().getTime(),id:obj.id},
          success:function(result){
              if(result.code == "200"){
                obj.customer =  result.data;
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
