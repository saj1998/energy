<template>
	<view scroll-y="true">
		<!-- 注意：class="chart-father" 必不可少，否则图表显示不出来 -->
		<view class="chart-father">
			<mpvue-echarts :echarts="echarts" :onInit="lineInit" canvasId="line"  />
		</view>
	</view>
</template>

<script>
	import * as echarts from '../../components/demo-echart/echarts/echarts.simple.min.js';
	import mpvueEcharts from '../../components/demo-echart/mpvue-echarts/src/echarts.vue';
	var lineChart=null;
	export default {
		components: {mpvueEcharts},
	    data() {
	        return {
				echarts: echarts
	        }
	    },
		methods: {
			lineInit(canvas, width, height) {
				lineChart = echarts.init(canvas, null, {
					width: width,
					height: height
				})
				canvas.setChart(lineChart)
				var option = {
					title: {
						text: '作业量'
					},
					tooltip: {
						trigger: 'axis'
					},
					legend: {
						data:['斗轮机','装船机','皮带机']
					},
					grid: {
						left: '3%',
						right: '4%',
						bottom: '3%',
						containLabel: true
					},
					toolbox: {
						feature: {
							saveAsImage: {}
						}
					},
					xAxis: {
						type: 'category',
						boundaryGap: false,
						data: ['一月','二月','三月','四月','五月','六月','']
					},
					yAxis: {
						type: 'value'
					},
					series: [
						{
							name:'斗轮机',
							type:'line',
							stack: '总量',
							data:[120, 132, 101, 134, 90, 230, 210]
						},
						{
							name:'装船机',
							type:'line',
							stack: '总量',
							data:[220, 182, 191, 234, 290, 330, 310]
						},
						{
							name:'皮带机',
							type:'line',
							stack: '总量',
							data:[150, 232, 201, 154, 190, 330, 410]
						}
					]
				};
				lineChart.setOption(option)
				return lineChart
			}
		}
	}
</script>

<style>
	.chart-father{
		display: flex;
		margin-top: -50upx;
		width: 100%;
		height: 500upx;
		background: #FFFFFF;
		justify-content: center;
	}
</style>
