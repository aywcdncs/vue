<template>
  <div>
   <div>

   <a href="javascript:void(0)" @click="add()"><i class="glyphicon glyphicon-plus"></i></a>

   <input type="text" placeholder="请输入要查询供应商编号" style="border: 1px gray solid; width: 200px; height: 30px; margin-left: 450px;" v-model="number">
   <button class="btn btn-default" @click="currentPage=1;getAll()"><i class="glyphicon glyphicon-search"></i>&nbsp;搜索</button>

    <br />


    <table class="table table-hover">
      <thead>
        <tr>
          <th>供应商编号</th>
          <th>供应商名字</th>
          <th>供应商电话</th>
          <th>供应商地址</th>
          <th>供应商等级</th>
          <th>相关操作</th>
        </tr>
      </thead>
     <tbody>
        <tr v-for="s in suppers">
          <td>{{s.suppNumber}}</td>
          <td>{{s.suppName}}</td>
          <td>{{s.suppPhone}}</td>
          <td>{{s.suppAddress}}</td>
          <td>{{s.suppliesNumber}}</td>
          <td>
            <a href="javascript:void(0)"><i class="glyphicon glyphicon-wrench"></i></a>
            <a href="javascript:void(0)" @click="del(s.id,s.suppNumber)"><i class="glyphicon glyphicon-trash"></i></a>
            <a href="javascript:void(0)"><i class="glyphicon glyphicon-align-justify"></i></a>
        </td>
        </tr>
      </tbody>
    </table>
   </div>

   <nav aria-label="Page navigation">
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
   </nav>

  </div>
</template>

<script>
  export default{
    data:function(){
      return {
        currentPage:1,
        pageSize:5,
        number:"",

        suppers:[],
        countPage:0
      }
    },
    computed:{
      indexs:function(){
        var obj = this;
        var arr = [];
        for(var i = 1;i<=obj.countPage;i++){
          arr[i-1]=i;
        }
        return arr;
      }
    },
    mounted() {
      this.getAll();
    },
    methods:{
      add:function(){
        this.$router.push("/main/addsupp")
      },
      del:function(id,suppNumber){
        var obj = this;
        if(confirm("你确定要删除供应商编号为"+suppNumber+"的供应商吗？")){
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/supplierinfoController/delete/"+id,
            data:{time:new Date().getTime()},
            success:function(result){
              alert(result);
               //重新查询
              obj.getAll();
            },
            xhrFields: {
              withCredentials: true
            }
          })
        }
      },
      toPage:function(currentPage){
        this.currentPage=currentPage;
        this.getAll();
      },
      getAll:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/supplierinfoController/getAll2",
          data:{time:new Date().getTime(),currentPage:obj.currentPage,pageSize:obj.pageSize,number:obj.number},
          success:function(result){
              if(result.code == "200"){
                obj.suppers =  result.data;
                obj.countPage =  result.countPage;
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
