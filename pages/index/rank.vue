<template>
	<view class="content">
		<view>
			<text class="title" ></text>
		</view>
		<table01></table01>
	</view>
</template>

<script>
	import table01 from "../tables/table01.vue"
	export default {
		components: {table01},
		data() {
			return {
				
			};
		},
		mounted() {
			
		},
		methods:{
			
		}
	}
</script>

<style>
	.content {
		margin-top: 50upx;
		text-align: center;
		height: 400upx;
	}

	.title {
		font-size: 36upx;
	}
</style>
