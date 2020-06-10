<template>
  <div>
   <div>
    <button class="btn btn-default" @click="toAadd()"><i class="glyphicon glyphicon-plus"></i>&nbsp;添加联系人</button>


   <input type="text" placeholder="请输入查询联系人的名字" style="border: 1px gray solid; width: 200px; height: 30px; margin-left: 450px;" v-model="searchName">
   <button class="btn btn-default" @click="currentPage=1;getAddresslists()"><i class="glyphicon glyphicon-search"></i>&nbsp;搜索</button>

    <br />


    <table class="table table-hover">
          <thead>
            <tr>
              <th>联系人id</th>
              <th>联系人姓名</th>
              <th>联系人性别</th>
              <th>联系人电话</th>
              <th>所在公司</th>
              <th>所在职位</th>
              <th>相关操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="c in addresslist">
              <td>{{c.id}}</td>
              <td>{{c.name}}</td>
              <td>{{c.sex == 0?"男":"女"}}</td>
              <td>{{c.phone}}</td>
              <td>{{c.company}}</td>
              <td>{{c.post}}</td>
              <td>
                <a href="javascript:void(0)" @click="toEdit(c.id)"><i class="glyphicon glyphicon-wrench"></i></a>
                <a href="javascript:void(0)" @click="del(c.id,c.name)"><i class="glyphicon glyphicon-trash"></i></a>
               
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

        addresslist:[],
        countPage:0,
      }
    },
    mounted:function(){
      this.getAddresslists();

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
        this.$router.push({name:"EditAddress",query:{'id':id}})
      },
      toAadd:function(){
        this.$router.push("/Addaddresslist")
      },
      del:function(id,name){
        var obj = this;
        if(confirm("你确定要删除"+name+"吗？")){
          $.ajax({
            type:"post",
            url:""+id,
            data:{time:new Date().getTime()},
            success:function(result){
              alert(result);
               //重新查询
              obj.getAddresslists();
            },
            xhrFields: {
              withCredentials: true
            }
          })
        }
      },
      

      toPage:function(currentPage){
        this.currentPage = currentPage;
        this.getAddresslists();
      },
      getAddresslists:function(){
          var obj = this;
          $.ajax({
            type:"post",
            url:"",
            data:{time:new Date().getTime(),currentPage:obj.currentPage,pageSize:obj.pageSize,searchName:obj.searchName},
            success:function(result){
                if(result.code == "220"){
                  obj.addresslists =  result.data;
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
