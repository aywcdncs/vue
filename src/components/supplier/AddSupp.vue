<template>
  <div>

  <h2>添加供应商</h2>
        <div class="form-horizontal">
          <div class="form-group">
            <label  class="col-sm-2 control-label">供应商编号</label>
            <div class="col-sm-10">
              <input type="text" class="form-control"  placeholder="请输入供应商编号" v-model="suppers.suppNumber">
            </div>
          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">供应商名字</label>
            <div class="col-sm-10">
               <input type="text" class="form-control"  placeholder="请输入供应商名字" v-model="suppers.suppName">
            </div>

          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">供应商电话</label>
            <div class="col-sm-10">
              <input type="email" class="form-control"  placeholder="请输入供应商电话" v-model="suppers.suppPhone">
            </div>
          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">供应商地址</label>
            <div class="col-sm-10">
              <input type="text" class="form-control"  placeholder="请输入供应商地址" v-model="suppers.suppAddress">
            </div>
          </div>
          <div class="form-group">
            <label  class="col-sm-2 control-label">供应商等级</label>
            <div class="col-sm-10">
              <input type="text" class="form-control"  placeholder="请输入供应商等级" v-model="suppers.suppliesNumber">
            </div>
          </div>

          <button class="btn btn-success"style="margin-left: 200px;" @click="add">添加</button>

        </div>


    </div>
</template>

<script>
  export default{
    data:function(){
      return {
        suppers:{suppNumber:"",suppName:"",suppPhone:"",suppAddress:"",suppliesNumber:""}
      }
    },
    methods:{
      add:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/supplierinfoController/add",
          data:{time:new Date().getTime(),suppNumber:obj.suppers.suppNumber,suppName:obj.suppers.suppName,suppPhone:obj.suppers.suppPhone,suppAddress:obj.suppers.suppAddress,suppliesNumber:obj.suppers.suppliesNumber},
          success:function(result){
             alert(result);
             //通过在JS代码进行页面跳转
             obj.$router.push("/main/supplierinfo");
          },
          xhrFields: {
              withCredentials: true
          }
        })
      }
    }
  }
</script>

<style>
</style>
