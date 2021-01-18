<template>
  <span class="tag" :class="selectedTheme">
    <span class="content" >{{ tag }} </span>
    <span class="close" @click="$emit('removeOneTagEvent', index)">x</span>
  </span>
</template>

<script>
export default {
  props: ["tag", "index", "tagColor"],
  data() {
    return {
      selectedTheme: "primary",
    };
  },
  created(){
    this.selectedTheme = this.tagColor
  }
};
</script>

<style lang="scss" scoped>
.primary {
  background-color: #cce5ff;
  color: #004085;
  border-color: #b8daff;
}
.success{
  background-color: #D5EDDB;
  border: 1px solid #c3e6cb;
  color: #155724;
}
.danger{
  background-color: #f8d7da;
  color: #721c24;
  border-color: #f5c6cb;
}
.tag {
  padding: 10px;

  cursor: default;
  font-size: 14px;
  margin-right: 5px;
  .close {
    cursor: pointer;
    font-size: 12px;
  }
}
</style>
