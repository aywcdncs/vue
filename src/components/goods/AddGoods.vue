<template>
  <div>
    <h3 style="margin-left: 5px;">添加商品 <span style="font-size: 4px;" ><a href="javascript:void(0)" @click="goBack()">返回--->></a></span></h3>
    <div class="form-horizontal">
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品编号</label>
        <div class="col-sm-10">
          <input type="text" class="form-control"  placeholder="请输入商品编号" v-model="goods.goodsNumber">
        </div>
      </div>
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品名称</label>
        <div class="col-sm-10">
           <input type="text" class="form-control"  placeholder="请输入商品名称" v-model="goods.goodsName">
        </div>
      </div>
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品价格</label>
        <div class="col-sm-10">
          <input type="email" class="form-control"  placeholder="请输入商品价格" v-model="goods.goodsPrice">
        </div>
      </div>
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品供应商</label>
        <div class="col-sm-10">
          <input type="text" class="form-control"  placeholder="请输入客户供应商" v-model="goods.goodsSuppname">
        </div>
      </div>
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品原产地</label>
        <div class="col-sm-10">
          <input type="text" class="form-control"  placeholder="请输入商品原产地" v-model="goods.goodsAddress">
        </div>
      </div>
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品生产日期</label>
        <div class="col-sm-10">
          <input type="text" class="form-control"  placeholder="请输入商品生产日期" v-model="goods.goodsDate">
        </div>
      </div>
      <div class="form-group">
        <label  class="col-sm-2 control-label">商品供应商编号</label>
        <div class="col-sm-10">
          <input type="text" class="form-control"  placeholder="请输入商品供应商编号" v-model="goods.goodsSuppernumber">
        </div>
      </div>


      <button class="btn btn-success" style="margin-left: 450px; margin-bottom: 5px;" @click="addGoods()">添加</button>

      </div>
  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        goods:{
          goodsNumber:"",
          goodsName:"",
          goodsPrice:"",
          goodsSuppname:"",
          goodsAddress:"",
          goodsDate:"",
          goodsSuppernumber:""
        }

      }
    },

    methods:{

      goBack:function(){
       this.$router.go(-1);
      },

      addGoods:function(){
        var obj = this;
          $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/goodsController/addGoods",
          data:{time:new Date().getTime(),goodsNumber:obj.goods.goodsNumber, goodsName:obj.goods.goodsName, goodsPrice:obj.goods.goodsPrice,
            goodsSuppname:obj.goods.goodsSuppernumber, goodsAddress:obj.goods.goodsAddress,goodsDate:obj.goods.goodsDate,
            goodsSuppernumber:obj.goods.goodsSuppernumber},
          success:function(result){
            alert(result);
            obj.$router.push("/main/goods");
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
