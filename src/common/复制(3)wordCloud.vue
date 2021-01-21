<template>
  <div >
    <div v-show="dataInfo.changeSign===true" id="container" ref="container"></div>
  </div>
</template>

<script>
import { WordCloud } from '@antv/g2plot';
	
export default {
  name: "",
  props: {
    dataObj: Object,
  },
  data() {
    return {
      dataInfo: {
  			changeSign:true,
				dataUrl:'https://gw.alipayobjects.com/os/antvdemo/assets/data/antv-keywords.json',
				imageMask:'https://gw.alipayobjects.com/mdn/rms_2274c3/afts/img/A*07tdTIOmvlYAAAAAAAAAAABkARQnAQ',
				wordField:'name',
				weightField:'value',
				colorField:'name',
//				interactions:[{ type: 'element-active' }],
//				state:{
//					active: {// 这里可以设置 active 时的样式
//	          style: {
//	            lineWidth: 3,
//	          },
//					}
//	  		},
//	  		wordStyle:{
//					fontFamily: 'Verdana',
//					fontSize: [8, 32],
//				},
  	}
  	}
  },
	mounted() {
//		this.showCloud(this.dataInfo)
			this.$nextTick(function () {
	      var tData = this.dataObj || this.dataInfo;
	      this.updateData(tData);
	    });
	},
  methods: {
showCloud(dat){
			fetch(dat.dataUrl)
				.then((res) => res.json())
				.then((data) => {
					dat.data=data
					const wordCloud = new WordCloud('container',dat);
//					if(dat.changeSign){
						wordCloud.render();
//					}else{
//						wordCloud.update(dat);
//					}
			});
		},
		updateData(newObj) {
			console.log('ZZZZZZZ',newObj)
      this.$nextTick(function () {
        this._updateData(newObj);
        this.$nextTick(function () {
        	const wordCloud = new WordCloud('container',newObj);
//      	this.showCloud(newObj)
//      	wordCloud.update(newObj)
        	wordCloud.update();
        	
//		    	for (var k in newObj) {
//		        if (arr.indexOf(k) !== -1) {
//		          for (var j in newObj[k]) {
//		            this.dataInfo[k][j] = newObj[k][j];
//		          }
//		        } else {
//		          this.dataInfo[k] = newObj[k];
//		        }
//		      }
		    	
        });
      });
		},
    _updateData(newObj) {
      for (var k in newObj) {
        this.$set(this.dataInfo, k, newObj[k]);
      }
      
//    for (var k in newObj) {
//      this.$set(this.data, k, newObj[k]);
//    }
    
    },
    created() {},
    beforeDestroy(){}
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
