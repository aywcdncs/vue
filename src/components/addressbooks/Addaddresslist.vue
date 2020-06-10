<template>
  <div>

  <h2>添加联系人</h2>
        <div class="form-horizontal">
          <div class="form-group">
            <label  class="col-sm-2 control-label">联系人姓名</label>
            <div class="col-sm-10">
              <input type="text" class="form-control"  placeholder="请输入联系人名字" v-model="addresslist.name">
            </div>
          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">联系人性别</label>
            <div class="col-sm-10">

              <input type="radio" name="sex"  class="but_sty" v-model="addresslist.sex">男
              <input type="radio" name="sex"  class="but_sty" v-model="addresslist.sex">女
            </div>

          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">联系人电话</label>
            <div class="col-sm-10">
              <input type="email" class="form-control"  placeholder="请输入联系人电话" v-model="addresslist.phone">
            </div>
          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">联系人所在公司</label>
            <div class="col-sm-10">
              <input type="text" class="form-control"  placeholder="请输入联系人所在公司" v-model="addresslist.company">
            </div>
          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">联系人所在职位</label>
            <div class="col-sm-10">
              <input type="text" class="form-control"  placeholder="请输入联系人所在职位" v-model="addresslist.post">
            </div>
            </div>
          <button class="btn btn-success" @click="add" style="margin-left: 200px;">添加</button>

        </div>


    </div>
</template>

<script>
  export default{
    data:function(){
    return{
      addresslist:{name:"",sex:0,phone:"",company:"",post:""}
    }
    },
    methods:{
      add:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/addresslistController/add",
          data:{time:new Date().getTime(),name:obj.addresslist.name,sex:obj.addresslist.sex,phone:obj.addresslist.phone,company:obj.addresslist.company,post:obj.addresslist.post},
          success:function(result){
             alert(result);
             //通过在JS代码进行页面跳转
             obj.$router.push("/main/addresslist");
          },
          xhrFields: {
              withCredentials: true
          }
        })
      }
    },
  }
</script>

<style>
  h2{
    color:yellowgreen
  }
  .but_sty{ border:0px; width:80px; height:30px; background-color:#333; font-size:12px; color:#fff;}


  .sex{
    font-size: 30px;
    color: blueviolet;
  }
</style>
