<template>
  <div style="padding: 20px 40px"> 
    <el-collapse v-model="activeNames" :accordion="true" style="width: 1000px">
      <el-collapse-item title="组件示例" name="1">
        <h2 style="position: relative; float: left; width: 100%">
          典型案例
          <el-button
            @click="openExampleStrunctDialog"
            style="float: right; margin-left: 20px"
            type="text"
            >参数数据结构</el-button
          >
          <el-button
            @click="openExampleCodeDialog"
            style="float: right"
            type="text"
            >示例代码</el-button
          >
        </h2>
        <Example1
          style="
            width: calc(100% - 180px);
            display: inline-block;
            float: left;
            margin-right: 20px;
          "
          ref="exampleItem"
          class="exampleItem"
        ></Example1>
        <el-radio-group
          v-model="exampleSelect"
          @change="dealSelectExample"
          style="
            padding: 10px 0px;
            float: left;
            width: 160px;
            display: inline-block;
          "
        >
          <slot v-for="d in exampleName">
            <el-radio
              style="width: 100%; margin: 0px; margin-bottom: 5px"
              :label="d.callbackName"
              border
              >{{ d.name }}</el-radio
            >
          </slot>
        </el-radio-group>
      </el-collapse-item>

      <el-collapse-item title="支持的事件" name="4">
        <DataTable ref="eventTable" :dataObj="eventDescription"></DataTable>
      </el-collapse-item>
      <el-collapse-item title="参数属性含义" name="5">
        <DataTable ref="paramTable" :dataObj="paramDescription"></DataTable>
      </el-collapse-item>
      <el-collapse-item title="支持的方法" name="6">
        <DataTable ref="methodTable" :dataObj="methodDescription"></DataTable>
      </el-collapse-item>
    </el-collapse>
    <DialogItem
      @openDialog="dealOpenDialog('exampleStrunctDialog')"
      @confirmDialog="dealConfirmDialog"
      :config="exampleStrunctDialog"
      ref="exampleStrunctDialog"
    >
      <template>
        <CodeViewer ref="exampleStructItem"></CodeViewer>
      </template>
    </DialogItem>
    <DialogItem
      @openDialog="dealOpenDialog('exampleCodeDialog')"
      :config="exampleCodeDialog"
      ref="exampleCodeDialog"
    >
      <template>
        <ExampleViewer
          style="max-height: 800px"
          :url="componentPath"
        ></ExampleViewer>
      </template>
    </DialogItem>
  </div>
</template>

<script>
import Example1 from "../../../static/example/sanKey/1.vue";
import ExampleViewer from "@/common/exampleViewer";
import CodeViewer from "@/common/codeViewer";
import DataTable from "@/common/dataTable";
import DialogItem from "@/common/dialogItem";

export default {
  components: {
    Example1,
    ExampleViewer,
    CodeViewer,
    DataTable,
    DialogItem,
  },
  mounted() {
    this.$nextTick(function () {
//    this.basicData1 = { ...this.$refs.exampleItem.dataObj.data[0] };
//    this.basicData2 = { ...this.$refs.exampleItem.dataObj.data[1] };
      this.basicData = { ...this.$refs.exampleItem.dataObj };
      
    });
  },
  data() {
    return {
      basicData: {},
      componentPath: "/static/example/wordCloud/1.vue",
      exampleSelect: "",
      activeNames: "1",
      exampleCodeDialog: {
        visible: false,
        title: "典型案例的示例代码",
        withFooter: false,
      },
      exampleStrunctDialog: {
        visible: false,
        title: "典型案例的参数数据结构",
        
        withFooter: true,
      },
      eventDescription: {
        header: [
          {
            prop: "name",
            label: "事件名",
            width: "180",
          },
          {
            prop: "description",
            label: "描述",
            align: "left",
          },
          {
            prop: "param",
            label: "参数",
            width: "180",
          },
        ],
        data: [
          {
            name: "on",
            param: "chart.on('eventName', callback);",
            description: "在 Chart 和 View 上通过 on 绑定事件。",
          },
          {
            name: "off",
            param: "chart.off('eventName', callback);",
            description: "在 Chart 和 View 上通过off 移除绑定事件。",
          },
        ],
      },
      paramDescription: {
        header: [
          {
            prop: "name",
            label: "属性名称",
            width: "180",
          },
          {
            prop: "description",
            label: "描述",
            align: "left",
          },
          {
            prop: "type",
            label: "类型",
            width: "120",
          },
          {
            prop: "option",
            label: "可选值",
            align: "center",
            width: "180",
          },
          {
            prop: "default",
            label: "默认值",
            align: "center",
            width: "120",
          },
        ],
        data: [
          {
            name: "data",
            description: "设置图表数据源。数据源为对象集合",
            type: "array object",
            required:true,
          },
          {
            name: "imageMask",
            description: "设置一张图片，然后图表就可以根据该图片的形状进行渲染，可以是图片元素实例或者 url 地址和 base64。注意： 词语只渲染在图片的深色部位，浅色的部位（如白色）不渲染词语。当使用图片的 url 地址时，图片的大小不宜过大，不然图片加载时间过长。",
            type: "HTMLImageElement | string",
            required:false,
          },
          {
            name: "wordStyle",
            description: "设置每个词语的样式",
            type: "object",
            required:false,
          },
          {
            name: "wordField",
            description: "单词内容在数据中所对应的字段名。",
            type: "string",
            required:true,
          },
          {
            name: "weightField",
            description: "单词所占权重在数据中所对应的字段名。",
            type: "string",
            required:true,
          },
          {
            name: "colorField",
            description: "根据该字段进行颜色映射。",
            type: "string",
            required:false,
          },
          {
            name: "random",
            description: "自定义所使用的随机函数，其值可以是一个 [0, 1) 区间中的值，也可以是一个返回该值的函数，当该值是一个固定的值时，每次渲染相同数据的词云图时，其对应的每个单词的布局坐标一致。",
            type: "number | function",
            required:false,
          },
          {
            name: "timeInterval",
            description: "设置绘制程序最大的执行时间，单位毫秒，如果时间设置过短可能会只绘制一部分词语。",
            type: "number",
            required:false,
            defalut:2000,
          },
          {
            name: "meta",
            description: "全局化配置图表数据元信息，以字段为单位进行配置。在 meta 上的配置将同时影响所有组件的文本信息。",
            type: "object",
            required:false,
            children:[
            	{
		            name: "alias",
		            description: " 	字段的别名。",
		            type: "string",
		          },
		          {
		            name: "formatter",
		            description: " 	callback 方法，对该字段所有值进行格式化处理。",
		            type: "function",
		          },
		          {
		            name: "values",
		            description: " 	枚举该字段下所有值。",
		            type: "string []",
		          },
		          {
		            name: "range",
		            description: " 	字段的数据映射区间，默认为[0,1]。",
		            type: "number []",
		          },
            ]
          },
        ],
      },
      methodDescription: {
        header: [
          {
            prop: "name",
            label: "方法名称",
            width: "180",
          },
          {
            prop: "description",
            label: "描述",
            align: "left",
          },
          {
            prop: "param",
            label: "参数",
            width: "180",
          },
        ],
        data: [
          {
            name: "render()",
            param: "-",
            description: "渲染图表。",
          },
          {
          	name:'update()',
          	param: "-",
            description: "更新图表配置项，配置覆盖，不会做差异比对。。",
          }
        ],
      },
      exampleName: [
        {
          name: "支付宝流量桑基图",
          callbackName: "exampleCallback1",
        },
        {
          name: "能量关系桑基图",
          callbackName: "exampleCallback2",
        },
        {
          name: "更新数据",
          callbackName: "exampleCallback3",
        },
      ],
    };
  },
  methods: {
  	updateExampleData(data) {
        if (this.$refs.exampleItem && this.$refs.exampleItem.updateData) {
          this.$refs.exampleItem.updateData(data);
        }
      },
    exampleCallback1() {
      var tData = { ...this.basicData }
      this.updateExampleData(tData);
    },
    exampleCallback2() {
      var tData = { ...this.basicData }
      console.log('410000000000000',tData)
      tData.data=[
  {
    "source": "Agricultural 'waste'",
    "target": "Bio-conversion",
    "value": 124.729
  },
  {
    "source": "Bio-conversion",
    "target": "Liquid",
    "value": 0.597
  },
  {
    "source": "Bio-conversion",
    "target": "Losses",
    "value": 26.862
  },
  {
    "source": "Bio-conversion",
    "target": "Solid",
    "value": 280.322
  },
  {
    "source": "Bio-conversion",
    "target": "Gas",
    "value": 81.144
  },
  {
    "source": "Biofuel imports",
    "target": "Liquid",
    "value": 35
  },
  {
    "source": "Biomass imports",
    "target": "Solid",
    "value": 35
  },
  {
    "source": "Coal imports",
    "target": "Coal",
    "value": 11.606
  },
  {
    "source": "Coal reserves",
    "target": "Coal",
    "value": 63.965
  },
  {
    "source": "Coal",
    "target": "Solid",
    "value": 75.571
  },
  {
    "source": "District heating",
    "target": "Industry",
    "value": 10.639
  },
  {
    "source": "District heating",
    "target": "Heating and cooling - commercial",
    "value": 22.505
  },
  {
    "source": "District heating",
    "target": "Heating and cooling - homes",
    "value": 46.184
  },
  {
    "source": "Electricity grid",
    "target": "Over generation / exports",
    "value": 104.453
  },
  {
    "source": "Electricity grid",
    "target": "Heating and cooling - homes",
    "value": 113.726
  },
  {
    "source": "Electricity grid",
    "target": "H2 conversion",
    "value": 27.14
  },
  {
    "source": "Electricity grid",
    "target": "Industry",
    "value": 342.165
  },
  {
    "source": "Electricity grid",
    "target": "Road transport",
    "value": 37.797
  },
  {
    "source": "Electricity grid",
    "target": "Agriculture",
    "value": 4.412
  },
  {
    "source": "Electricity grid",
    "target": "Heating and cooling - commercial",
    "value": 40.858
  },
  {
    "source": "Electricity grid",
    "target": "Losses",
    "value": 56.691
  },
  {
    "source": "Electricity grid",
    "target": "Rail transport",
    "value": 7.863
  },
  {
    "source": "Electricity grid",
    "target": "Lighting & appliances - commercial",
    "value": 90.008
  },
  {
    "source": "Electricity grid",
    "target": "Lighting & appliances - homes",
    "value": 93.494
  },
  {
    "source": "Gas imports",
    "target": "Ngas",
    "value": 40.719
  },
  {
    "source": "Gas reserves",
    "target": "Ngas",
    "value": 82.233
  },
  {
    "source": "Gas",
    "target": "Heating and cooling - commercial",
    "value": 0.129
  },
  {
    "source": "Gas",
    "target": "Losses",
    "value": 1.401
  },
  {
    "source": "Gas",
    "target": "Thermal generation",
    "value": 151.891
  },
  {
    "source": "Gas",
    "target": "Agriculture",
    "value": 2.096
  },
  {
    "source": "Gas",
    "target": "Industry",
    "value": 48.58
  },
  {
    "source": "Geothermal",
    "target": "Electricity grid",
    "value": 7.013
  },
  {
    "source": "H2 conversion",
    "target": "H2",
    "value": 20.897
  },
  {
    "source": "H2 conversion",
    "target": "Losses",
    "value": 6.242
  },
  {
    "source": "H2",
    "target": "Road transport",
    "value": 20.897
  },
  {
    "source": "Hydro",
    "target": "Electricity grid",
    "value": 6.995
  },
  {
    "source": "Liquid",
    "target": "Industry",
    "value": 121.066
  },
  {
    "source": "Liquid",
    "target": "International shipping",
    "value": 128.69
  },
  {
    "source": "Liquid",
    "target": "Road transport",
    "value": 135.835
  },
  {
    "source": "Liquid",
    "target": "Domestic aviation",
    "value": 14.458
  },
  {
    "source": "Liquid",
    "target": "International aviation",
    "value": 206.267
  },
  {
    "source": "Liquid",
    "target": "Agriculture",
    "value": 3.64
  },
  {
    "source": "Liquid",
    "target": "National navigation",
    "value": 33.218
  },
  {
    "source": "Liquid",
    "target": "Rail transport",
    "value": 4.413
  },
  {
    "source": "Marine algae",
    "target": "Bio-conversion",
    "value": 4.375
  },
  {
    "source": "Ngas",
    "target": "Gas",
    "value": 122.952
  },
  {
    "source": "Nuclear",
    "target": "Thermal generation",
    "value": 839.978
  },
  {
    "source": "Oil imports",
    "target": "Oil",
    "value": 504.287
  },
  {
    "source": "Oil reserves",
    "target": "Oil",
    "value": 107.703
  },
  {
    "source": "Oil",
    "target": "Liquid",
    "value": 611.99
  },
  {
    "source": "Other waste",
    "target": "Solid",
    "value": 56.587
  },
  {
    "source": "Other waste",
    "target": "Bio-conversion",
    "value": 77.81
  },
  {
    "source": "Pumped heat",
    "target": "Heating and cooling - homes",
    "value": 193.026
  },
  {
    "source": "Pumped heat",
    "target": "Heating and cooling - commercial",
    "value": 70.672
  },
  {
    "source": "Solar PV",
    "target": "Electricity grid",
    "value": 59.901
  },
  {
    "source": "Solar Thermal",
    "target": "Heating and cooling - homes",
    "value": 19.263
  },
  {
    "source": "Solar",
    "target": "Solar Thermal",
    "value": 19.263
  },
  {
    "source": "Solar",
    "target": "Solar PV",
    "value": 59.901
  },
  {
    "source": "Solid",
    "target": "Agriculture",
    "value": 0.882
  },
  {
    "source": "Solid",
    "target": "Thermal generation",
    "value": 400.12
  },
  {
    "source": "Solid",
    "target": "Industry",
    "value": 46.477
  },
  {
    "source": "Thermal generation",
    "target": "Electricity grid",
    "value": 525.531
  },
  {
    "source": "Thermal generation",
    "target": "Losses",
    "value": 787.129
  },
  {
    "source": "Thermal generation",
    "target": "District heating",
    "value": 79.329
  },
  {
    "source": "Tidal",
    "target": "Electricity grid",
    "value": 9.452
  },
  {
    "source": "UK land based bioenergy",
    "target": "Bio-conversion",
    "value": 182.01
  },
  {
    "source": "Wave",
    "target": "Electricity grid",
    "value": 19.013
  },
  {
    "source": "Wind",
    "target": "Electricity grid",
    "value": 289.366
  }
];

       tData.sourceField= 'source'
      tData.targetField= 'target'
      tData.weightField= 'value'
      tData.color= ['red', 'green', 'yellow']
      tData.edgeStyle= {
        fill: '#ccc',
        fillOpacity: 0.4,
      },
      console.log(tData)
      this.updateExampleData(tData);
    },
    exampleCallback3() {
      var tData = { ...this.basicData }
      tData.data=[{
						source: '注入数据1',
						target: '主要流向',
						value: 160
					},
					{
						source: '注入数据2',
						target: '主要流向',
						value: 40
					},
					{
						source: '注入数据3',
						target: '主要流向',
						value: 10
					},
					{
						source: '注入数据4',
						target: '主要流向',
						value: 10
					},
					{
						source: '注入数据5',
						target: '主要流向',
						value: 8
					},
					{
						source: '注入数据6',
						target: '主要流向',
						value: 27
					},
					{
						source: '注入数据7',
						target: '主要流向',
						value: 30
					},
					{
						source: '主要流向',
						target: '流出数据1',
						value: 40
					},
					{
						source: '主要流向',
						target: '流出数据2',
						value: 35
					},
					{
						source: '主要流向',
						target: '流出数据3',
						value: 25
					},
					{
						source: '主要流向',
						target: '流出数据4',
						value: 10
					},
					{
						source: '主要流向',
						target: '流出数据5',
						value: 30
					},
					{
						source: '主要流向',
						target: '流出数据6',
						value: 40
					},
					{
						source: '主要流向',
						target: '流出数据7',
						value: 42
					},
					{
						source: '主要流向',
						target: '其他流向',
						value: 45
					},
					
				];
      this.updateExampleData(tData);
    },
    dealSelectExample(v) {
      console.log(v);
      if (v && typeof this[v] === "function") {
        this[v]();
      }
    },
    openDataStrunctDialog() {
      this.$refs.testDialog.show();
    },
    openExampleStrunctDialog() {
      this.$refs.exampleStrunctDialog.show();
    },
    openExampleCodeDialog() {
      this.$refs.exampleCodeDialog.show();
    },
    dealOpenDialog(name) {
      if (name === "testDialog") {
        this.$refs.exampleViewerItem.code = beautify(
          JSON.stringify(this.$refs.exampleItem.dataObj),
          opts
        );
      } else if (name === "exampleStrunctDialog") {
        this.$refs.exampleStructItem.code = beautify(
          JSON.stringify(this.$refs.exampleItem.dataObj),
          opts
        );
      } else {
      }
    },
    dealConfirmDialog() {
      var code = this.$refs.exampleStructItem.code;
//    console.log(code);
      try {
        this.updateExampleData(JSON.parse(code));
        // this.$refs.exampleTest.$forceUpdate();
        this.exampleSelect = "";
      } catch (e) {
        console.log(e);
      }
    },
    dealSelectionChange(val) {},
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.introduce {
  position: relative;
  float: left;
  max-width: 1200px;
  margin-bottom: 20px;
  padding-right: 20px;
  width: 100%;
}

.introduce > h2 {
  font-weight: 700;
  margin-bottom: 5px;
}

/deep/ .CodeMirror {
  border-top: solid 1px #ddd;
  border-left: solid 1px #ddd;
  box-shadow: 1px 1px 1px #ddd;
  height: 500px !important;
}

/deep/ .exampleItem,
.howToImport .CodeMirror {
  height: auto !important;
}

.exampleItem {
  padding-bottom: 10px;
}

/deep/ .containerArea {
  margin-bottom: 10px;
}

/deep/ .el-form-item {
  margin-bottom: 5px;
}

/deep/ .el-collapse-item__header {
  font-weight: 700;
}
</style>
