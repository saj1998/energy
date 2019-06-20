<template>
	<view class="content">
		<picker @change="bindPickerChange" :value="index" :range="array" range-key="devname">
			<view class="uni-input" placeholder="设备名称">{{array[index].devname}}</view>
		</picker>
		<input type="text" v-model="cause" placeholder="故障原因"></input>
		
		<input type="text" v-model="faulttime" placeholder="故障持续时间"></input>
		<input type="text" v-model="faultuser" placeholder="报告人"></input>
		
		<button type="primary" @click="fault">添加</button>
	</view>
</template>

<script>
	import uniIcon from "@dcloudio/uni-ui/lib/uni-icon/uni-icon.vue"
	export default {
		components: {
			uniIcon
		},
		data() {
			return {
				cause:'',
				faulttime:'',
				faultuser:'',
				devid: "",
				array: [{devname:''}],
				index: 0
			}
		},
		onLoad() {
			uni.request({
				url: this.url + 'baseDevice/list',
				header: {
					'custom-header': 'register'
				},
				success: (res) => {
					this.array = res.data;
				},
				fail: () => {
					uni.showToast({
						icon: 'none',
						title: '网络异常,请稍后重试',
						duration: 1000
					});
				}
			})
		},
		methods: {
			bindPickerChange(e) {
				this.index = e.target.value;
			},
			changeSex(obj) {
				this.sex = obj.detail.value;
			},
			fault() {
				if (this.faulttime.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入故障时间',
						duration: 1000
					});
					return;
				}
				if (this.cause.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入故障原因',
						duration: 1000
					});
					return;
				}
				if (this.faultuser.length <= 0) {
					uni.showToast({
						icon: 'none',
						title: '请输入报告人',
						duration: 1000
					});
					return;
				}
				
				
				//网络请求
				uni.request({
					url: this.url + 'produceFault/insert',
					data: {
						cause: this.cause,
						faulttime: this.faulttime,
						faultuser: this.faultuser,
						devid: this.array[this.index].devid
					},
					header: {
						'custom-header': 'register'
					},
					success: (res) => {
						uni.showToast({
							icon: 'success',
							title: '添加成功',
							duration: 1000
						});
					},
					fail: () => {
						uni.showToast({
							icon: 'none',
							title: '网络异常,请稍后重试',
							duration: 1000
						});
					}
				})
			}
		}
	}
</script>

<style>
	input{
		background: white;
		width: 90%;
		height: 100upx;
		padding-left: 30upx;
		margin: 5upx 5%;
	}
</style>
