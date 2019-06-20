<template>
	<!-- 选项卡组件 -->
	<view class="content">
		<view>
			<wuc-tab :tab-list="tabList" :tabCur.sync="TabCur" @change="tabChange" textFlex='true'></wuc-tab>
			<view v-if="TabCur==0">
				<synchro></synchro>
			</view>
			<view v-else-if="TabCur==1">
				<phones></phones>
			</view>
			<view v-else>
				<fault></fault>
			</view>
		</view>
	</view>
</template>

<script>
	import WucTab from '@/components/wuc-tab/wuc-tab.vue';
	import synchro from "../yw/synchro.vue"
	import phones from "../home/phones.vue"
	import fault from "../yw/fault.vue"
	export default {
		data() {
			return {
			  TabCur: 0,
			  tabList: [{ name: '数据采集' }, { name: '通讯录' }, { name: '故障记录' }],
			}},
		components: { WucTab,synchro,phones,fault },
		methods: {
			tabChange(index) {
				this.TabCur = index;
			}
		}
	}
</script>

<style>
	@import url("../../static/css/yw.css");
</style>
