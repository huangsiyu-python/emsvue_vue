<template>
    <div id="wrap">
			<div id="top_content">
				<div id="header">
					<div id="rightheader">
                    <el-button type="success" @click="user_del()">注销登录</el-button>
					</div>
					<div id="topheader">
						<h1 id="title">
							<a href="#">main</a>
						</h1>
					</div>
					<div id="navigation">
					</div>
				</div>
				<div id="content">
					<p id="whereami">
					</p>
					<h1>
						欢迎{{user_msg}}进入员工管理系统
					</h1>
					<table class="table">
						<tr class="table_header">
							<td>ID</td>
							<td>Name</td>
							<td>Photo</td>
							<td>Salary</td>
							<td>Age</td>
							<td>Operation</td>
						</tr>
						<tr v-for="(emp,index) in emp_list" :key="emp.id" :class="index%2==0?'row1':'row2'">
							<td>{{emp.id}}</td>
							<td>{{emp.emp_name}}</td>
							<td><img :src="emp.img" style="height: 60px;"></td>
							<td>{{emp.salary}}</td>
							<td>{{emp.age_name}}</td>
							<td>
                                <!--<a href="javascript:;" @click="delEmp(emp.id)">删除员工</a>&nbsp;-->
                                <a href="javascript:void(0)" @click="delemp(emp.id)">删除员工</a>
                                <!--<a href="javascript:;"@click="editEmp(emp.id)">修改员工</a>-->
                                <router-link :to="'/update/'+emp.id">修改员工</router-link>
                            </td>
						</tr>
					</table>
					<p>
						<!--<input type="button" class="button" value="Add Employee"/>-->
                        <el-button type="success"><router-link to="/add">添加员工</router-link></el-button>
					</p>
				</div>
			</div>
			<div id="footer">
				<div id="footer_bg">
				ABC@126.com
				</div>
			</div>
		</div>
</template>

<script>
    export default {
        name: "Index",
        data(){
          return{
              user_msg:"",
              emp_list:[],
          }
        },
        methods:{
          findAllEmp(){
              this.$axios.get("http://127.0.0.1:8000/api/emp/").then(res=>{
                  console.log(res.data.results);
                  this.emp_list=res.data.results;
              }).catch(error=>{
                  this.$message.error(("查询出错了"))
              })
          },
            delemp(emp_id){
              console.log(emp_id);
              this.$axios({
                url: "http://127.0.0.1:8000/api/emp/"+`${emp_id}/`,
                method: "delete",
              }).then(res=>{
                console.log(res.data.results);
                location.reload()
              }).catch(error=>{
                 this.$message.error("删除出错了");
              })
},
            user_del(){
            sessionStorage.clear();
            this.$router.push("/login")
        },
            },
            editEmp(id){
            },
        created() {
           let username= sessionStorage.getItem("user");
           this.user_msg=username;
           console.log(username);
            if(username){

            }else {
                this.$message.error("请登录");
                this.$router.push("/login")
            }
            this.findAllEmp();
        }

    }
</script>

<style scoped>

</style>
