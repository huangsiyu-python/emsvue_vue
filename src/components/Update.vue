<template>
    <div id="wrap">
			<div id="top_content">
					<div id="header">
						<div id="rightheader">
							<p>
								2009/11/20
								<br />
							</p>
						</div>
						<div id="topheader">
							<h1 id="title">
								<a href="#">Main</a>
							</h1>
						</div>
						<div id="navigation">
						</div>
					</div>
				<div id="content">
					<p id="whereami">
					</p>
					<h1>
						update Emp info:{{$route.params.id}}
					</h1>
					<!--<form>-->
						<table cellpadding="0" cellspacing="0" border="0"
							class="form_table">
							<tr>
								<td valign="middle" align="right">id:</td>
								<td valign="middle" align="left">{{$route.params.id}}</td>
							</tr>
							<tr>
								<td valign="middle" align="right">name:</td>
								<td valign="middle" align="left"><input type="text" class="inputgri" name="name" v-model="emp.emp_name"/></td>
							</tr>
							<tr>
								<td valign="middle" align="right">photo:</td>
								<td valign="middle" align="left"><input type="file" name="photo" ref="photo" /></td>
							</tr>
							<tr>
								<td valign="middle" align="right">salary:</td>
								<td valign="middle" align="left"><input type="text" class="inputgri" name="salary" v-model="emp.salary" /></td>
							</tr>
							<tr>
								<td valign="middle" align="right">age:</td>
								<td valign="middle" align="left"><input type="text" class="inputgri" name="age" v-model="emp.age"/></td>
							</tr>
						</table>
						<p>
							<input type="submit" class="button" value="修改" @click="upEmp" />
						</p>
					<!--</form>-->
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
        name: "Update",
        data(){
            return{
            emp_id:"",
                emp:{},
            }
        },
        methods:{
        get_emp_id(id){
            let emp_id=this.$route.params.id;
            console.log(emp_id);
            this.$axios.get("http://127.0.0.1:8000/api/emp/"+`${emp_id}/`).then(res=>{
                console.log(res.data);
                this.emp=res.data.results;
                console.log(this.emp)
            }).catch(error=>{
            this.$message.error("错误")
            })
        },
            upEmp(){
            let emp_id=this.$route.params.id;
            let formData=new FormData;
            formData.append("emp_name",this.emp.emp_name);
            formData.append("salary",this.emp.salary);
            formData.append("age",this.emp.age);
            let photo=this.$refs.photo.files[0];
            if(photo){
                formData.append("img",photo)
            }
            this.$axios({
                url:"http://127.0.0.1:8000/api/emp/"+`${emp_id}/`,
                method:"put",
                data:formData,
                headers:{
                  'content-type':'multipart/form-data'
                },
            }).then(res=>{
                this.$message("修改成功");
                this.$router.push("/index")
            }).catch(error=>{
                this.$message.error("修改失败");
                // this.$router.push('/index')
            })
            },
        },
        created() {
           this.get_emp_id()
        }

    }
</script>

<style scoped>

</style>
