<template>
  <div>
    <draggable
      v-model="myArray"
      group="people"
      @start="drag = true"
      @end="drag = false"
      item-key="id"
    >
      <template #item="{ element }">
        <div>{{ element.name }}</div>
        <div>123122313</div>
      </template>
    </draggable>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable,
  },
  data() {
    return {
      drag: false,
      myArray:[]
    };
  },
};
</script>

<style lang="scss" scoped>
</style>