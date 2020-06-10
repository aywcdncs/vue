<template>
  <div>
          <h2>修改联系人信息 {{id}}</h2>
          <div class="form-group row" style="width: 100%;">
              <label class="col-form-label">联系人名字</label>
              <div>
                <input type="text" class="form-control" v-model="addresslist.name">
              </div>
           </div>

           <div class="form-group row" style="width: 100%;">
               <label class="col-form-label">联系人性别</label>
               <div>
                 <input type="radio" name="sex" value="0" class="but_sty" v-model="addresslist.sex"><span class="sex">男</span>
                 <input type="radio" name="sex" value="1" class="but_sty" v-model="addresslist.sex"><span class="sex">女</span>
               </div>
            </div>

            <div class="form-group row" style="width: 100%;">
                <label class="col-form-label">联系人电话</label>
                <div>
                  <input type="text" class="form-control"  v-model="addresslist.phone">
                </div>
             </div>

             <div class="form-group row" style="width: 100%;">
                 <label class="col-form-label">联系人公司</label>
                 <div>
                   <input type="text" class="form-control" v-model="addresslist.company">
                 </div>
              </div>
              <div class="form-group row" style="width: 100%;">
                  <label class="col-form-label">联系人职位</label>
                  <div>
                    <input type="text" class="form-control" v-model="addresslist.post">
                  </div>
               </div>

               <button class="btn btn-info" @click="update">修改</button>
  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        id:this.$route.query.id,
        addresslist:{}
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
          url:"http://localhost:8082/crm/addresslistController/update",
          data:{time:new Date().getTime(),id:obj.addresslist.id,name:obj.addresslist.name,sex:obj.addresslist.sex,phone:obj.addresslist.phone,company:obj.addresslist.company,post:obj.addresslist.post},
          success:function(result){
             alert(result);
             //通过在JS代码进行页面跳转
             obj.$router.push("/main/addresslist");
          },
          xhrFields: {
            withCredentials: true
          }
        });
      },
      getById:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/addresslistController/getAddresslistById",
          data:{time:new Date().getTime(),id:obj.id},//
          success:function(result){
            if(result.code == "220"){
              obj.addresslist=result.data;//
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
