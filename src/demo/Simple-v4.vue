<template>
  <div>
    <div ref="myPage" class="my-graph" style="height:calc(100vh);">
      <div style="position: absolute;left:10px;top:10px;background-color: rgba(255,255,255, 0.3);border-radius: 10px;font-size: 12px;color: #ffffff;padding:10px;">
        Fully customize the graphical elements of the graph using div+css、Vue components,、and React components through slots
        <br />
        通过【插槽】使用div+css、Vue组件、React组件完全自定义图形元素。
      </div>
      <RelationGraph
        ref="graphRef"
        :options="graphOptions">
        <template #node="{node}">
          <div>
            <button class="icon-btn" :class="['icon-btn--' + node.data.iconColor]" type="button">
              <span class="icon-btn__back"></span>
              <span class="icon-btn__front">
                <i style="font-size: 30px;" :class="node.data.icon" />
              </span>
              <span class="icon-btn__label">{{node.text}}</span>
            </button>
          </div>
        </template>
      </RelationGraph>
    </div>
  </div>
</template>

<script>
// 如果您没有在main.js文件中使用Vue.use(RelationGraph); 就需要使用下面这一行代码来引入relation-graph
// import RelationGraph from 'relation-graph';

export default {
  name: 'Demo4NodeStyle',
  components: { },
  data() {
    return {
      graphOptions: {
        allowSwitchLineShape: true,
        allowSwitchJunctionPoint: true,
        defaultLineColor: 'rgba(255, 255, 255, 0.6)',
        defaultNodeColor: 'transparent',
        defaultNodeBorderWidth: 0,
        defaultNodeBorderColor: 'transpanret',
        defaultNodeFontColor: '#ffffff',
        defaultNodeShape: 1,
        toolBarDirection: 'h',
        toolBarPositionH: 'right',
        toolBarPositionV: 'bottom',
        defaultPloyLineRadius: 10,
        defaultLineShape: 1,
        // defaultJunctionPoint: 'lr',
        disableNodeClickEffect: true,
        layout: {
          layoutName: 'force',
          from: 'left',
          min_per_width: 410, // 根据节点的宽度设置，这个是让图谱看起来偏亮的关键
          min_per_height: 90,
        }
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
        'rootId': 'a',
        'nodes': [
          { 'id': 'a', 'text': 'a', data: { iconColor: 'yellow', icon: 'el-icon-star-on' } },
          { 'id': 'b', 'text': 'b', data: { iconColor: 'yellow', icon: 'el-icon-star-on' } },
          { 'id': 'b1', 'text': 'b1', data: { iconColor: 'yellow', icon: 'el-icon-star-on' } },
          { 'id': 'b1-1', 'text': 'b1-1', data: { iconColor: 'blue', icon: 'el-icon-user-solid' } },
          { 'id': 'b1-2', 'text': 'b1-2', data: { iconColor: 'blue', icon: 'el-icon-user-solid' } },
          { 'id': 'b1-3', 'text': 'b1-3', data: { iconColor: 'blue', icon: 'el-icon-user-solid' } },
          { 'id': 'b1-4', 'text': 'b1-4', data: { iconColor: 'blue', icon: 'el-icon-s-promotion' } },
          { 'id': 'b1-5', 'text': 'b1-5', data: { iconColor: 'blue', icon: 'el-icon-s-promotion' } },
          { 'id': 'b1-6', 'text': 'b1-6', data: { iconColor: 'blue', icon: 'el-icon-s-promotion' } },
          { 'id': 'b2', 'text': 'b2', data: { iconColor: 'red', icon:'el-icon-basketball' }},
          { 'id': 'b2-1', 'text': 'b2-1', data: { iconColor: 'red', icon:'el-icon-basketball'} },
          { 'id': 'b2-2', 'text': 'b2-2', data: { iconColor: 'red', icon:'el-icon-basketball'} },
          { 'id': 'c', 'text': 'c', data: { iconColor: 'purple', icon: 'el-icon-potato-strips' } },
          { 'id': 'c1', 'text': 'c1', data: { iconColor: 'purple', icon: 'el-icon-potato-strips' } },
          { 'id': 'c2', 'text': 'c2', data: { iconColor: 'purple', icon: 'el-icon-potato-strips' } },
          { 'id': 'c3', 'text': 'c3', data: { iconColor: 'purple', icon: 'el-icon-potato-strips' } }],
        'lines': [
          { 'from': 'a', 'to': 'b', text: '' },
          { 'from': 'b', 'to': 'b1', text: '' },
          { 'from': 'b1', 'to': 'b1-1', text: '' },
          { 'from': 'b1', 'to': 'b1-2', text: '' },
          { 'from': 'b1', 'to': 'b1-3', text: '' },
          { 'from': 'b1', 'to': 'b1-4', text: '' },
          { 'from': 'b1', 'to': 'b1-5', text: '' },
          { 'from': 'b1', 'to': 'b1-6', text: '' },
          { 'from': 'b', 'to': 'b2', text: '' },
          { 'from': 'b2', 'to': 'b2-1', text: '' },
          { 'from': 'b2', 'to': 'b2-2', text: '' },
          { 'from': 'a', 'to': 'c', text: '' },
          { 'from': 'c', 'to': 'c1', text: '' },
          { 'from': 'c', 'to': 'c2', text: '' },
          { 'from': 'c', 'to': 'c3', text: '' }]
      };
      this.$refs.graphRef.setJsonData(__graph_json_data, (graphInstance) => {
        // 这些写上当图谱初始化完成后需要执行的代码
      });
    }
  }
};
</script>
<style lang="scss" scoped>
::v-deep .rel-map {
  background: none !important;
  .rel-node-shape-1 {
  }
}
::v-deep .rel-toolbar{
  color: #ffffff;
  .c-current-zoom{
    color: #ffffff;
  }
}
.my-graph{
  background: linear-gradient(to right, rgb(16, 185, 129), rgb(101, 163, 13));
}
</style>

<style lang="scss" scoped>


.icon-btn {
  border: none;
  background-color: transparent;
  outline: transparent;
  position: relative;
  width: 4.5em;
  height: 4.5em;
  perspective: 24em;
  transform-style: preserve-3d;
  -webkit-tap-highlight-color: transparent
}

.icon-btn__back,.icon-btn__front,.icon-btn__label {
  transition: opacity var(--trans-dur) cubic-bezier(0.83,0,0.17,1),transform var(--trans-dur) cubic-bezier(0.83,0,0.17,1)
}

.icon-btn__back,.icon-btn__front {
  border-radius: 1.25em;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%
}

.icon-btn__back {
  background: linear-gradient(hsl(var(--hue),10%,50%),hsl(208,10%,50%));
  box-shadow: .5em -0.5em .75em hsla(var(--hue),10%,10%,0.15);
  display: block;
  transform: rotate(15deg);
  transform-origin: 100% 100%
}

.icon-btn__front {
  background-color: hsla(0,0%,100%,0.3);
  box-shadow: 0 0 0 .125em hsla(0,0%,100%,0.3) inset;
  backdrop-filter: blur(0.75em);
  -webkit-backdrop-filter: blur(0.75em);
  display: flex;
  transform-origin: 80% 50%;
  color: #ffffff;
  align-items: center;
  justify-content: center;
  & svg {
    width:70%;
    height:70%;
  }
}

//.icon-btn--blue .icon-btn__back {
//  background: linear-gradient(hsl(var(--hue),90%,50%),hsl(208,90%,50%))
//}

//.icon-btn--yellow .icon-btn__back {
//  background: linear-gradient(hsl(43,90%,50%),hsl(28,90%,50%))
//}
.icon-btn--blue .icon-btn__back {
  background: linear-gradient(hsl(253,90%,50%),hsl(238,90%,50%))
}

.icon-btn--purple .icon-btn__back {
  background: linear-gradient(hsl(283,90%,50%),hsl(268,90%,50%))
}

.icon-btn--red .icon-btn__back {
  background: linear-gradient(hsl(3,90%,50%),hsl(348,90%,50%))
}

.icon-btn--yellow .icon-btn__back {
  background: linear-gradient(hsl(43,90%,50%),hsl(28,90%,50%))
}

.icon-btn__icon {
  margin: auto;
  width: 1.5em;
  height: 1.5em
}

.icon-btn__label {
  font-size: .75em;
  line-height: 2;
  opacity: 0;
  position: absolute;
  top: 100%;
  right: 0;
  left: 0;
  transform: translateY(0);
  color: #ffffff;
}

.icon-btn:focus-visible .icon-btn__back,.icon-btn:hover .icon-btn__back {
  transform: rotate(22.5deg)
}

.icon-btn:focus-visible .icon-btn__front,.icon-btn:hover .icon-btn__front {
  transform: translateZ(3em) rotateX(20deg) rotateY(20deg)
}

.icon-btn:focus-visible .icon-btn__label,.icon-btn:hover .icon-btn__label {
  opacity: 1;
  transform: translateY(20%)
}
</style>
