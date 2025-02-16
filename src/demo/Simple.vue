<template>
  <div>
    <div ref="myPage" style="height:calc(100vh);">
      <RelationGraph
        ref="graphRef"
        :options="graphOptions"
        :on-node-click="onNodeClick"
        :on-line-click="onLineClick">
		<template #node="{node}">
          <div @mouseover="showNodeTips(node, $event)" @mouseout="hideNodeTips(node, $event)" @touchstart="showNodeTips(node, $event)" @touchend="hideNodeTips(node, $event)">
            <div class="c-my-rg-node">
              <i style="font-size: 30px;" :class="node.data.myicon"> {{ node.id }}</i>
            </div>
          </div>
        </template>
      </RelationGraph>
	   <div v-show="isShowNodeTipsPanel" :style="{left: nodeMenuPanelPosition.x + 'px', top: nodeMenuPanelPosition.y + 'px' }" style="z-index: 999;padding:10px;background-color: #ffffff;border:#eeeeee solid 1px;box-shadow: 0px 0px 8px #cccccc;position: absolute;border-radius: 10px;">
		  <div style="line-height: 25px;padding-left: 10px;color: #888888;font-size: 12px;">节点名称：{{currentNode.text}}</div>
		  <div class="c-node-menu-item">ID:{{currentNode.id}}</div>
		  <div class="c-node-menu-item">姓名:{{currentNode.text}}</div>
		  <div class="c-node-menu-item">性别:{{currentNodeData.sex}}</div>
		  <div class="c-node-menu-item">生日:{{currentNodeData.birthday}}</div>
		  <div class="c-node-menu-item">年龄:{{currentNodeData.age}}</div>
		  <div class="c-node-menu-item">生肖:{{currentNodeData.zodiac_name}}</div>
		  <div class="c-node-menu-item">头像:<img :src="currentNodeData.image" width="120" height="120" /></div>
		</div>
  </div>
  </div>
</template>

<script>
// 如果您没有在main.js文件中使用Vue.use(RelationGraph); 就需要使用下面这一行代码来引入relation-graph
// import RelationGraph from 'relation-graph';
export default {
  name: 'Demo',
  components: { },
  data() {
    return {
      isShowCodePanel: false,
      isShowNodeTipsPanel: false,
	    isShowNodeMenuPanel: false,
      nodeMenuPanelPosition: { x: 0, y: 0 },
      currentNode: {},
	  currentNodeData: {},
      graphOptions: {
        allowSwitchLineShape: true,
        allowSwitchJunctionPoint: true,
        defaultNodeColor: 'rgba(66,187,66,1)',
        defaultJunctionPoint: 'border',
        isNeedShowAutoLayoutButton: true,
        showSingleNode: true,
        showNodeLabel: true,
        showNodeShortLabel: true,
        defaultLineWidth: 1,
        defaultExpandHolderPosition: "bottom",
        defaultLineShape: 0,
        useAnimationWhenRefresh: false,
        isMoveByParentNode: true,

		layout:
          {
            label: 'center',
			      layoutName: 'force',
            layoutClassName: 'seeks-layout-force',

          },
      }
    };
  },
  mounted() {
    this.showGraph();
  },
  methods: {
    showGraph() {
      const __graph_json_data = {
        rootId: '2',
        nodes: [
          // 注意：在节点配置信息中，你的自定义属性需要像下面这样放到data标签中，否则数据会丢失
{'id': '0', 'text': 'root', 'data': {'sex': '无', 'birthday': '1900-01-01', 'age': '125', 'zodiac_name': '鼠-Rat', 'image': './image/qq.jpeg'}},
{'id': '1', 'text': '人员1', 'data': {'sex': '男', 'birthday': '1949-01-01', 'age': '76', 'zodiac_name': '牛-Ox', 'image': './image/qq.jpeg'}},
{'id': '2', 'text': '人员2', 'data': {'sex': '女', 'birthday': '1959-01-02', 'age': '66', 'zodiac_name': '猪-Pig', 'image': './image/qq.jpeg'}},
{'id': '3', 'text': '人员3', 'data': {'sex': '男', 'birthday': '1969-01-02', 'age': '56', 'zodiac_name': '鸡-Rooster', 'image': './image/qq.jpeg'}},
{'id': '4', 'text': '人员4', 'data': {'sex': '女', 'birthday': '1979-01-03', 'age': '46', 'zodiac_name': '羊-Goat', 'image': './image/qq.jpeg'}},
{'id': '5', 'text': '人员5', 'data': {'sex': '男', 'birthday': '1989-01-03', 'age': '36', 'zodiac_name': '蛇-Snake', 'image': './image/qq.jpeg'}},
{'id': '6', 'text': '人员6', 'data': {'sex': '女', 'birthday': '1999-01-04', 'age': '26', 'zodiac_name': '兔-Rabbit', 'image': './image/qq.jpeg'}},
{'id': '7', 'text': '人员7', 'data': {'sex': '男', 'birthday': '2009-01-04', 'age': '16', 'zodiac_name': '牛-Ox', 'image': './image/qq.jpeg'}},
{'id': '8', 'text': '人员8', 'data': {'sex': '女', 'birthday': '2019-01-05', 'age': '6', 'zodiac_name': '猪-Pig', 'image': './image/qq.jpeg'}},
{'id': '9', 'text': '人员9', 'data': {'sex': '男', 'birthday': '2029-01-05', 'age': '-4', 'zodiac_name': '鸡-Rooster', 'image': './image/qq.jpeg'}},
{'id': '10', 'text': '人员10', 'data': {'sex': '女', 'birthday': '2039-01-06', 'age': '-14', 'zodiac_name': '羊-Goat', 'image': './image/qq.jpeg'}},
{'id': '11', 'text': '人员11', 'data': {'sex': '男', 'birthday': '2049-01-06', 'age': '-24', 'zodiac_name': '蛇-Snake', 'image': './image/qq.jpeg'}},
{'id': '12', 'text': '人员12', 'data': {'sex': '女', 'birthday': '2059-01-07', 'age': '-34', 'zodiac_name': '兔-Rabbit', 'image': './image/qq.jpeg'}},
{'id': '13', 'text': '人员13', 'data': {'sex': '男', 'birthday': '2069-01-07', 'age': '-44', 'zodiac_name': '牛-Ox', 'image': './image/qq.jpeg'}},
{'id': '14', 'text': '人员14', 'data': {'sex': '女', 'birthday': '2079-01-08', 'age': '-54', 'zodiac_name': '猪-Pig', 'image': './image/qq.jpeg'}},
{'id': '15', 'text': '人员15', 'data': {'sex': '男', 'birthday': '2089-01-08', 'age': '-64', 'zodiac_name': '鸡-Rooster', 'image': './image/qq.jpeg'}},
{'id': '16', 'text': '人员16', 'data': {'sex': '女', 'birthday': '2099-01-09', 'age': '-74', 'zodiac_name': '羊-Goat', 'image': './image/qq.jpeg'}},
        ],
        lines: [
{'from': '0', 'to': '1', 'text': '1'},
{'from': '1', 'to': '2', 'text': '子'},
{'from': '1', 'to': '3', 'text': '女'},
{'from': '1', 'to': '4', 'text': '亲'},
{'from': '0', 'to': '5', 'text': '1'},
{'from': '5', 'to': '6', 'text': '子'},
{'from': '5', 'to': '7', 'text': '女'},
{'from': '5', 'to': '8', 'text': '子'},
{'from': '5', 'to': '9', 'text': '女'},
{'from': '0', 'to': '10', 'text': '1'},
{'from': '10', 'to': '11', 'text': '子'},
{'from': '10', 'to': '12', 'text': '女'},
{'from': '10', 'to': '13', 'text': '子'},
{'from': '10', 'to': '14', 'text': '女'},
{'from': '10', 'to': '15', 'text': '子'},
{'from': '10', 'to': '16', 'text': '女'},
        ]
      };
      this.$refs.graphRef.setJsonData(__graph_json_data, (graphInstance) => {
        // 这些写上当图谱初始化完成后需要执行的代码
      });
    },
    onNodeClick(nodeObject, $event) {
      console.log('onLineClick:', this.currentNode.data, 'this.nodeMenuPanelPosition.x:', this.nodeMenuPanelPosition.x);

    },
    onLineClick(lineObject, linkObject, $event) {
      console.log('onLineClick:', lineObject.data);
    },
    showNodeTips(nodeObject, $event) {
      this.currentNode = nodeObject;
      const _base_position = this.$refs.myPage.getBoundingClientRect();
      console.log('showNodeMenus:', $event.clientX, $event.clientY, _base_position);
      this.isShowNodeTipsPanel = true;
	  this.currentNodeData = nodeObject.data;
      this.nodeMenuPanelPosition.x = $event.clientX - _base_position.x + 10;
      this.nodeMenuPanelPosition.y = $event.clientY - _base_position.y + 10;
    },
    hideNodeTips(nodeObject, $event) {
      this.isShowNodeTipsPanel = false;
    }
  }
};
</script>

<style lang="scss">

</style>

<style lang="scss" scoped>
.c-my-rg-node {
  height:80px;line-height: 80px;border-radius: 50%;cursor: pointer;
  display: flex;
  place-items: center;
  justify-content: center;
}
.c-node-menu-item{
  line-height: 30px;padding-left: 10px;cursor: pointer;color: #444444;font-size: 14px;border-top:#efefef solid 1px;
}
.c-node-menu-item:hover{
  background-color: rgba(66,187,66,0.2);
}

::v-deep .relation-graph {
  .my-node-style {
    background-color: #00ced1 !important; /** 通过自定义样式设置节点颜色需要加 !important **/
  }

  .my-node-style:hover {
    background-color: #ff0000 !important;
  }

  @keyframes myFlash {
    from {
      opacity: 1.0;
    }
    50% {
      opacity: 0.4;
    }
    to {
      opacity: 1.0;
    }
  }

  @-webkit-keyframes myFlash {
    from {
      opacity: 1.0;
    }
    20% {
      opacity: 0.1;
    }
    60% {
      opacity: 0.5;
    }
    to {
      opacity: 1.0;
    }
  }

  .my-node-flash-style {
    animation: myFlash 600ms infinite;
    -webkit-animation: myFlash 2000ms infinite;
  }
}

</style>
