<template>
  <div>
    <div style="height:calc(100vh);">
      <RelationGraph
        ref="graphRef"
        :options="graphOptions"
        :on-node-click="onNodeClick"
        :on-line-click="onLineClick" />
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
      graphOptions: {
        // 这里可以参考"Graph 图谱"中的参数进行设置
      }
    };
  },
  mounted() {
    this.showGraph();
  },
  methods: {
    showGraph() {
      const __graph_json_data = {
        rootId: 'a',
        nodes: [
          { id: 'a', text: 'Border color', borderColor: 'yellow' },
          { id: 'a1', text: 'No border', borderWidth: -1, color: '#ff8c00' },
          { id: 'a2', text: 'Plain', borderWidth: 3, color: 'transparent', borderColor: '#ff8c00', fontColor: '#ff8c00' },
            // 除非万不得已，否则不建议使用html属性，你可以使用node插槽，让节点展示为任意形态
          { id: 'a1-1', html: '<span style="color:#ff8c00">Text Node</span>' },
          { id: 'a1-4', html: '<div style="border:#ff8c00 solid 2px;height:80px;width:80px;border-radius: 40px;background-image: url(/images/rg-logo.png);background-position: center center;" />', nodeShape: 0 },
          { id: 'b', text: 'Font color', color: '#43a2f1', fontColor: '#ffd700' },
          { id: 'd', text: 'Node Size', width: 150, height: 150, color: '#ff8c00', borderWidth: 5, borderColor: '#ffd700', fontColor: '#ffffff' },
          { id: 'e', text: 'Rectangular node', nodeShape: 1 },
          { id: 'f', text: 'Rectangular', borderWidth: 1, nodeShape: 1, width: 300, height: 60 },
          { id: 'f1', text: 'Fixed', fixed: true, x: 60, y: 60 },
          { id: 'g', text: 'Css Flash', styleClass: 'my-node-flash-style' }
        ],
        lines: [
          { from: 'a', to: 'b' },
          { from: 'a', to: 'c' },
          { from: 'a', to: 'a1' },
          { from: 'a1', to: 'a1-1' },
          { from: 'a', to: 'a2' },
          { from: 'a1', to: 'a1-4' },
          { from: 'a', to: 'f1' },
          { from: 'a', to: 'd' },
          { from: 'd', to: 'f' },
          { from: 'a', to: 'g' },
          { from: 'a', to: 'e' },
          { from: 'b', to: 'e' }
        ]
      };
      this.$refs.graphRef.setJsonData(__graph_json_data, (graphInstance) => {
        // 这些写上当图谱初始化完成后需要执行的代码
      });
    },
    onNodeClick(nodeObject, $event) {
      console.log('onNodeClick:', nodeObject);
    },
    onLineClick(lineObject, linkObject, $event) {
      console.log('onLineClick:', lineObject);
    }
  }
};
</script>

<style lang="scss" scoped>
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
