<template>
  <div>
  	<WordCloud
  		:dataObj="dataObj"
      ref="exampleTestItem"
      >
      </WordCloud>
  </div>
</template>

<script>
import WordCloud from "@/common/wordCloud";
export default {
  name: '',
  data(){
  	return {
  		dataObj:{
					changeSign:true,
					data:[{
							"value": 9,
							"name": "AntV"
						},

						{
							"value": 8,
							"name": "F2"
						},
						{
							"value": 8,
							"name": "G2"
						},
						{
							"value": 8,
							"name": "G6"
						},
						{
							"value": 8,
							"name": "DataSet"
						},
						{
							"value": 8,
							"name": "墨者学院"
						},

						{
							"value": 6,
							"name": "Analysis"
						},
						{
							"value": 6,
							"name": "Data Mining"
						},
						{
							"value": 6,
							"name": "Data Vis"
						},
						{
							"value": 6,
							"name": "Design"
						},
						{
							"value": 6,
							"name": "Grammar"
						},
						{
							"value": 6,
							"name": "Graphics"
						},
						{
							"value": 6,
							"name": "Graph"
						},
						{
							"value": 6,
							"name": "Hierarchy"
						},
						{
							"value": 6,
							"name": "Labeling"
						},
						{
							"value": 6,
							"name": "Layout"
						},
						{
							"value": 6,
							"name": "Quantitative"
						},
						{
							"value": 6,
							"name": "Relation"
						},
						{
							"value": 6,
							"name": "Statistics"
						},
						{
							"value": 6,
							"name": "可视化"
						},
						{
							"value": 6,
							"name": "数据"
						},
						{
							"value": 6,
							"name": "数据可视化"
						},

						{
							"value": 4,
							"name": "Arc Diagram"
						},
						{
							"value": 4,
							"name": "Bar Chart"
						},
						{
							"value": 4,
							"name": "Canvas"
						},
						{
							"value": 4,
							"name": "Chart"
						},
						{
							"value": 4,
							"name": "DAG"
						},
						{
							"value": 4,
							"name": "DG"
						},
						{
							"value": 4,
							"name": "Facet"
						},
						{
							"value": 4,
							"name": "Geo"
						},
						{
							"value": 4,
							"name": "Line"
						},
						{
							"value": 4,
							"name": "MindMap"
						},
						{
							"value": 4,
							"name": "Pie"
						},
						{
							"value": 4,
							"name": "Pizza Chart"
						},
						{
							"value": 4,
							"name": "Punch Card"
						},
						{
							"value": 4,
							"name": "SVG"
						},
						{
							"value": 4,
							"name": "Sunburst"
						},
						{
							"value": 4,
							"name": "Tree"
						},
						{
							"value": 4,
							"name": "UML"
						}],
					imageMask:'',
					wordField:'name',
					weightField:'value',
					colorField:'name',
//					interactions:[{ type: 'element-active' }],
//					state:{
//						active: {// 这里可以设置 active 时的样式
//		          style: {
//		            lineWidth: 3,
//		          },
//						}
//					},
//					wordStyle:{
//							fontFamily: 'Verdana',
//							fontSize: [8, 32],
//					},
			}
  	}
  },
	components: {
		WordCloud,
//  WordCloud: () => import("@/common/wordCloud"),
	},
	beforeMount(){},
	mounted() {},
	methods: {
    updateData(data) {
      this.dataObj = data;
      this.$refs.exampleTestItem.updateData(this.dataObj);
    },


  },
}
</script>
