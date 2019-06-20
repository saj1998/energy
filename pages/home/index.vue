<template>
	<view class="content">
			<uni-segmented-control :current="current" :values="items" @clickItem="onClickItem" style-type="text" active-color="#4cd964"></uni-segmented-control>
			<view class="comps">
				<view v-show="current === 0">
					<energy></energy>
				</view>
				<view v-show="current === 1">
					<produce></produce>
				</view>
				<view v-show="current === 2">
					<rank></rank>
				</view>
			</view>
	</view>
</template>

<script>
	import uniSegmentedControl  from "@dcloudio/uni-ui/lib/uni-segmented-control/uni-segmented-control.vue"
	import energy from "../index/energy.vue"
	import produce from "../index/produce.vue"
	import rank from "../index/rank.vue"
	export default {
		components: {uniSegmentedControl,energy,produce,rank},
		data() {
			return {
				items: ['能耗','产销','排名'],
				current: 0
			}
		},
		onLoad() {

		},
		methods: {
			onClickItem(index) {
				if (this.current !== index) {
					this.current = index;
				}
			}
		}
	}
</script>

<style>
	@import url("../../static/css/index.css");
</style>
