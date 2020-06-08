<template>
  <div>
   <div>
    <button class="btn btn-default" @click="toAadd()"><i class="glyphicon glyphicon-plus"></i>&nbsp;添加客户</button>


   <input type="text" placeholder="请输入查询客户的名字" style="border: 1px gray solid; width: 200px; height: 30px; margin-left: 450px;" v-model="searchName">
   <button class="btn btn-default" @click="currentPage=1;getCustomers()"><i class="glyphicon glyphicon-search"></i>&nbsp;搜索</button>

    <br />


    <table class="table table-hover">
          <thead>
            <tr>
              <th>客户编号</th>
              <th>客户名字</th>
              <th>客户年龄</th>
              <th>客户邮箱</th>
              <th>客户电话</th>
              <th>相关操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="c in customers">
              <td>{{c.id}}</td>
              <td>{{c.name}}</td>
              <td>{{c.age}}</td>
              <td>{{c.email}}</td>
              <td>{{c.phone}}</td>
              <td>
                <a href="javascript:void(0)" @click="toEdit(c.id)"><i class="glyphicon glyphicon-wrench"></i></a>
                <a href="javascript:void(0)" @click="del(c.id,c.name)"><i class="glyphicon glyphicon-trash"></i></a>
                <a href="javascript:void(0)" @click="detailsCustomer(c.id)"><i class="glyphicon glyphicon-align-justify"></i></a>
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
        searchName:"",

        customers:[],
        countPage:0,
      }
    },
    mounted:function(){
      this.getCustomers();

    },

    computed:{

      indexs:function(){
        var obj = this;
        var arr=[];
        for(var i = 1;i<=obj.countPage;i++){
          arr[i-1] = i;
        }
        return arr;
      }
    },
    methods:{
      toEdit:function(id){
        this.$router.push({name:"EditCustomer",query:{'id':id}})
      },
      toAadd:function(){
        this.$router.push("/addCustomer")
      },
      del:function(id,name){
        var obj = this;
        if(confirm("你确定要删除"+name+"吗？")){
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/customerController/delete/"+id,
            data:{time:new Date().getTime()},
            success:function(result){
              alert(result);
               //重新查询
              obj.getCustomers();
            },
            xhrFields: {
              withCredentials: true
            }
          })
        }
      },
      detailsCustomer:function(id){
        this.$router.push({name:"DetailsCustomer",query:{id:id}});
      },

      toPage:function(currentPage){
        this.currentPage = currentPage;
        this.getCustomers();
      },
      getCustomers:function(){
          var obj = this;
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/customerController/getCustomers",
            data:{time:new Date().getTime(),currentPage:obj.currentPage,pageSize:obj.pageSize,searchName:obj.searchName},
            success:function(result){
                if(result.code == "200"){
                  obj.customers =  result.data;
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
