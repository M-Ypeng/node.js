<template>
  <!--ele ui table +  sortablejs -->
  <!-- 表格拖动 -->
  <div>
    <el-table row-key="id" :data="tableData" style="width: 100%">
      <el-table-column
        v-for="(item, index) in tableHead"
        :key="index"
        :prop="item.prop"
        :label="item.label"
        :show-overflow-tooltip="true"
      />
    </el-table>
  </div>
</template>
<script>
import Sortable from "sortablejs";
export default {
  components: {},
  data() {
    return {
      drag: false, // 是否拖拽
      tableHead: [
        {
          prop: "name",
          label: "姓名",
        },
        {
          prop: "age",
          label: "年龄",
        },
        {
          prop: "sex",
          label: "性别",
        },
      ],
      tableData: [
        {
          id: 1,
          name: "小明",
          age: "18",
          sex: "男",
        },
        {
          id: 2,
          name: "小红",
          age: "20",
          sex: "女",
        },
        {
          id: 3,
          name: "小白",
          age: "15",
          sex: "男",
        },
      ],
    };
  },
  mounted() {
    this.rowDrag();
    this.columnDrop();
  },
  methods: {
    //列拖拽
    columnDrop() {
      const wrapperTr = document.querySelector(".el-table__header-wrapper tr");
      this.sortable = Sortable.create(wrapperTr, {
        animation: 180,
        delay: 0,
        filter: ".cannotDrag",
        onEnd: (evt) => {
          const oldItem = this.tableHead[evt.oldIndex];
          this.tableHead.splice(evt.oldIndex, 1);
          this.tableHead.splice(evt.newIndex, 0, oldItem);
        },
      });
    },
    // 行拖拽
    rowDrag() {
      const tbody = document.querySelector(".el-table__body-wrapper tbody");
      const that = this;
      Sortable.create(tbody, {
        onEnd({ newIndex, oldIndex }) {
          const currentRow = that.tableData.splice(oldIndex, 1)[0];
          that.tableData.splice(newIndex, 0, currentRow);
        },
      });
    },
  },
};
</script>

<style lang="scss" scoped>
</style>