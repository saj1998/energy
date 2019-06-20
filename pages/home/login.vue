<template>
	<view class="content">
		<view>
			<input type="text" placeholder="请输入用户名" v-model="username"/>
			<view>
			<input type="password" placeholder="请输入密码" v-model="password"/>
			<!-- <uni-icon type="eye" size="20" @click='fn'></uni-icon> -->
			</view>
		
			<button  @click="login">登录</button>
			<button  @click="register">注册</button>
		</view>
		
	</view>
</template>

<script>
	import uniIcon from "@dcloudio/uni-ui/lib/uni-icon/uni-icon.vue"
	export default {
		components: {uniIcon},
		data() {
			return {
				username:'lhx',
				password:'123456',
				flag:true	
			};
		},
		mounted() {
			
		},
		methods:{
			register(){
				uni.navigateTo({
					url: 'register'
				});
			},
			fn(){
				this.flag=!this.flag;
			},
			
			/* 与后台交互 */
		login(){
			if (this.username.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入用户名'
					});
					return;
				}
				if (this.password.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入密码'
					});
					return;
				}
			
				uni.request({
					url: this.url+"baseUser/login", //仅为示例，并非真实接口地址。
					data: {
						username: this.username,
						password: this.password
					},
					header: {
						'custom-header': 'hello' //自定义请求头信息
					},
					success: (res) => {
						if(res.data){
							uni.setStorage({
								key: 'baseUser',
								data: res.data
							});
							uni.switchTab({
								url:'index'
							});
							uni.showToast({
								title: '登录成功',
								duration: 2000
							});
							
						}else{
							uni.showToast({
								title: '登录失败',
								duration: 2000
							});
						}
						
					}
				});
			},
			onNavigationBarButtonTap(){  
				uni.navigateTo({
					url: 'register'
				});		  
			}
			
		}
	}
</script>

<style>
	@import url("../../static/css/login.css");
	
</style>
