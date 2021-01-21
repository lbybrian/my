<template>
	<div>
		<div id="container" ref="container"></div>
	</div>
</template>

<script>
	import { Sankey } from '@antv/g2plot';

	export default {
		name: "",
props: {
		dataObj: Object,
	},
	data() {
		return {
			dataInfo: {
				data: [{
						source: '首次打开2131',
						target: '首页 UV123',
						value: 160
					},
					{
						source: '结果页21',
						target: '首页 UV2313',
						value: 40
					},
					{
						source: '验证页213',
						target: '首页 UV231',
						value: 10
					},
					{
						source: '我的123',
						target: '首页 UV123',
						value: 10
					},
					{
						source: '朋友1231',
						target: '首页 UV2131',
						value: 8
					},
					{
						source: '其他来源123',
						target: '首页 UV312',
						value: 27
					},
					{
						source: '首页 UV123',
						target: '理财12312',
						value: 30
					},
					{
						source: '首页 UV3123',
						target: '扫一扫12123',
						value: 40
					},
					{
						source: '首页 UV21321',
						target: '服务13',
						value: 35
					},
					{
						source: '首页 UV1233',
						target: '蚂蚁森林12312',
						value: 25
					},
					{
						source: '首页 UV1231',
						target: '跳失2131',
						value: 10
					},
					{
						source: '首页 UV123',
						target: '借呗3123',
						value: 30
					},
					{
						source: '首页 UV123',
						target: '花呗231',
						value: 40
					},
					{
						source: '首页 UV21321',
						target: '其他流向123',
						value: 45
					},
				],
				sourceField:'source',
				targetField: 'target',
				weightField: 'value',
				nodeWidthRatio: 0.008,
				nodePaddingRatio: 0.03,
				
				}
			}
		},

		mounted() {
			this.$nextTick(function() {
				var tData = this.dataObj || this.dataInfo;
				this.updateData(tData);
			});
		},

		methods: {
			updateData(){
				if(this.sankey){
					this.sankey.destroy()
				}
				let DATA=this.dataInfo.data;
//				let DATA=this.dataObj.data?this.dataObj.data:this.dataInfo.data;
				let elem = this.$refs.container;
				this.sankey = new Sankey(elem, {
					data: DATA,
					sourceField: 'source',
					targetField: 'target',
					weightField: 'value',
					nodeWidthRatio: 0.008,
					nodePaddingRatio: 0.03,
//			      	color: ['red', 'green', 'yellow'],
//			      	edgeStyle: {
//				        fill: '#ccc',
//				        fillOpacity: 0.4,
//			      	},
				});
				this.sankey.render();
			},
		},
	};
</script>

<style scoped>
	.containerArea {
		width: 100%;
		height: 100%;
	}
	
	/deep/ .el-pagination {
		padding-left: 0px;
	}
</style>