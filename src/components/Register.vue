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
						注册
					</h1>
						<table cellpadding="0" cellspacing="0" border="0"
							class="form_table">
							<tr>
								<td valign="middle" align="right">
									用户名:
								</td>
								<td valign="middle" align="left">
									<input type="text" class="inputgri" name="username" v-model="username" />
								</td>
							</tr>
							<tr>
								<td valign="middle" align="right">
									真实姓名:
								</td>
								<td valign="middle" align="left">
									<input type="text" class="inputgri" name="name" v-model="real_name" @blur=""/>
								</td>
							</tr>
							<tr>
								<td valign="middle" align="right">
									密码:
								</td>
								<td valign="middle" align="left">
									<input type="password" class="inputgri" name="pwd" v-model="password" />
								</td>
							</tr>
                            <tr>
								<td valign="middle" align="right">
									确认密码:
								</td>
								<td valign="middle" align="left">
									<input type="password" class="inputgri" name="re_pwd" v-model="re_pwd" />
								</td>
							</tr>
							<tr>
								<td valign="middle" align="right">
									性别:
								</td>
								<td valign="middle" align="left">
									男
									<input type="radio" class="inputgri" name="sex" value="m" checked="checked" @click="gender=0"/>
									女
									<input type="radio" class="inputgri" name="sex" value="f" @click="gender=1"/>
								</td>
							</tr>

						</table>
						<p>
							<!--<input type="submit" class="button" value="注册" />-->
                            <el-button type="success" @click="user_register">注册</el-button>
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
        name: "Register",
        data(){
            return{
                username:"",
                password:"",
                real_name:"",
                re_pwd:"",
                gender:"",
            }
        },
        methods:{
            user_register(){
                this.$axios({
                    url:"http://127.0.0.1:8000/api/user/",
                    method: "post",
                    data:{
                        username:this.username,
                        password:this.password,
                        re_pwd:this.re_pwd,
                        real_name:this.real_name,
                        gender:this.gender,
                    }
                }).then(res=>{
                    console.log(res.data['message']);
                    if (res.data['message']){
                        this.$message("注册成功");
                        this.$router.push(("/login"))
                    }
                }).catch(error=>{
                    console.log(error);
                    this.$message.error("注册失败")
                })
            }
        }
    }
</script>

<style scoped>

</style>
