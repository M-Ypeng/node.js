<template>
  <div class="mainBox">
    <!-- <div>{{ drag ? "拖拽中" : "拖拽停止" }}</div> -->
    <div>课程表</div>
    <!--使用draggable组件-->

    <div>
      <div class="item_box">周一</div>
      <div class="item_box">周一</div>
      <div class="item_box">周三</div>
      <div class="item_box">周四</div>
      <div class="item_box">周五</div>
      <div class="item_box">周六</div>
      <div class="item_box">周日</div>
    </div>

    <div>
      <draggable
        v-model="myArray"
        chosenClass="chosen"
        forceFallback="true"
        group="people"
        animation="500"
        @start="onStart"
        @end="onEnd"
      >
        <transition-group>
          <div
            class="item_box otherBox"
            v-for="element in myArray"
            :key="element.id"
          >
            {{ element.name }}
          </div>
        </transition-group>
      </draggable>
    </div>
  </div>
</template>
<style scoped>
/*被拖拽对象的样式*/
.mainBox {
  margin: 0 auto;
  width: 1050px;
  height: 45px;
  line-height: 45px;
  background: #fdfdfd;
  height: 600px;
}
.item_box {
  background-color: pink;
  display: inline-block;
  width: 130px;
  margin: 0 10px;
}
.otherBox {
  margin-top: 20px;
}
.box {
  width: 200px;
  display: inline-block;
  margin-top: 10px;
  padding: 6px;
  background-color: #fdfdfd;
  border: solid 1px #eee;
  margin-bottom: 10px;
  cursor: move;
}
/*选中样式*/
.chosen {
  border: solid 1px #3089dc !important;
}
</style>
<script>
import draggable from "vuedraggable";
export default {
  //注册draggable组件
  components: {
    draggable,
  },
  data() {
    return {
      drag: false,
      //定义要被拖拽对象的数组
      myArray: [
        { people: "cn", id: 1, name: "语文" },
        { people: "cn", id: 2, name: "小黄" },
        { people: "cn", id: 3, name: "语文" },
        { people: "us", id: 4, name: "小马" },
        { people: "cn", id: 5, name: "语文" },
        { people: "cn", id: 6, name: "语文" },
        { people: "cn", id: 7, name: "语文" },

        { people: "cn", id: 8, name: "语文" },
        { people: "cn", id: 9, name: "小黄" },
        { people: "cn", id: 10, name: "语文" },
        { people: "us", id: 11, name: "英语" },
        { people: "cn", id: 12, name: "小1" },
        { people: "cn", id: 13, name: "英语" },
        { people: "cn", id: 14, name: "小3" },
      ],
    };
  },
  methods: {
    //开始拖拽事件
    onStart() {
      this.drag = true;
    },
    //拖拽结束事件
    onEnd() {
      this.drag = false;
    },
  },
};
</script>
