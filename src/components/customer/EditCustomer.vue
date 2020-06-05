<template>
  <div>
          <h2>修改客户信息 {{id}}</h2>
          <div class="form-group row" style="width: 100%;">
              <label class="col-form-label">客户名字</label>
              <div>
                <input type="text" class="form-control" v-model="customer.name">
              </div>
           </div>

           <div class="form-group row" style="width: 100%;">
               <label class="col-form-label">客户性别</label>
               <div>
                 <input type="radio" name="sex" value="0" class="but_sty" v-model="customer.sex"><span class="sex">男</span>
                 <input type="radio" name="sex" value="1" class="but_sty" v-model="customer.sex"><span class="sex">女</span>
               </div>
            </div>

            <div class="form-group row" style="width: 100%;">
                <label class="col-form-label">客户电话</label>
                <div>
                  <input type="text" class="form-control"  v-model="customer.phone">
                </div>
             </div>

             <div class="form-group row" style="width: 100%;">
                 <label class="col-form-label">客户生日</label>
                 <div>
                   <input type="text" class="form-control" v-model="customer.birth">
                 </div>
              </div>

               <button class="btn btn-info" @click="update">修改</button>
  </div>
</template>

<script>
 export default{
      data:function(){
        return {
          //把id带过来,通过id回显
          //路由传递参数之在组件中接收参数
          id:this.$route.query.id,
          customer:{}
        }
      },
      mounted:function(){
        this.getById();
      },
      methods:{
        update:function(){
          var obj = this;
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/customerController/update",
            data:{time:new Date().getTime(),id:obj.customer.id,name:obj.customer.name,sex:obj.customer.sex,phone:obj.customer.phone,birth:obj.customer.birth},
            success:function(result){
               alert(result);
               //通过在JS代码进行页面跳转
               obj.$router.push("/main/customer");
            },
            xhrFields: {
              withCredentials: true
            }
          });
        },
        //通过id查询客户
        getById:function(){
          var obj = this;
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/customerController/getCustomerById",
            data:{time:new Date().getTime(),id:obj.id},//
            success:function(result){
              if(result.code == "200"){
                obj.customer=result.data;//
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
