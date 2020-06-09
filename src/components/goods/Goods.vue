<template>
 <div>
  <div>
   <button @click="toAddGoods()" class="btn btn-default" style="width: 200px; margin-top: 5px; margin-left: 5px;" ><i class="glyphicon glyphicon-plus"></i>&nbsp;添加商品</button>

   <br />
   <table class="table table-hover" style="text-align: center;">
         <thead>
           <tr>
             <th>商品ID</th>
             <th>商品编号</th>
             <th>商品名称</th>
             <th>商品价格</th>
             <th>商品供应商</th>
             <th>商品原产地</th>
             <th>商品生产日期</th>
             <th>商品供应商编号</th>
             <th>相关信息</th>
           </tr>
         </thead>
         <tbody>
           <tr v-for="g in goods">
             <td>{{g.id}}</td>
             <td>{{g.goodsNumber}}</td>
             <td>{{g.goodsName}}</td>
             <td>{{g.goodsPrice}}</td>
             <td>{{g.goodsSuppname}}</td>
             <td>{{g.goodsAddress}}</td>
             <td>{{g.goodsDate}}</td>
             <td>{{g.goodsSuppernumber}}</td>
             <td>
              <a href="#"><i class="glyphicon glyphicon-trash" @click="delGoods(g.id)"></i></a>
              <a href="#"><i class="glyphicon glyphicon-wrench" ></i></a>
              <a href="javascript:void(0)" ><i class="glyphicon glyphicon-align-justify"></i></a>
             </td>
          </tr>
         </tbody>
       </table>
  </div>


  <!-- <nav aria-label="Page navigation">
    <ul class="pagination">
      <li>
        <a href="javascript:void(0)" aria-label="Previous" @click="toPage(1)">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li v-for="index in indexs"><a href="javascript:void(0)" @click="toPage(index)">{{index}}</a></li>
      <li>
        <a href="javascript:void(0)" aria-label="Next" @click="toPage(countPage)">
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>

      <li ><a href="javascript:void(0)">总共{{countPage}}页，当前第{{currentPage}}页</a></li>
    </ul>
  </nav> -->

  </div>
</template>

<script>
  export default{
    data:function(){
      return {
       goods:[]
      }
    },
    mounted: function(){
        this.getAllGoods();
    },
    methods:{


      delGoods:function(id){
        var obj = this;
        if(confirm("你确定删除吗？")){
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/goodsController/delGoods/"+id,
            data:{time:new Date().getTime()},
            success:function(result){
              alert(result);
              obj.getAllGoods();
            },
            xhrFields: {
              withCredentials: true
            }

          });

        }


      },



      toAddGoods:function(){
        this.$router.push("/main/addGoods");
      },
      getAllGoods:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/goodsController/getAllGoods",
          data:{time:new Date().getTime()},
          success:function(result){
            if(result.code == "200"){
              obj.goods = result.data;
            }
          },
          xhrFields: {
            withCredentials: true
          }

        });
      }
    },


}
</script>

<style>
</style>
