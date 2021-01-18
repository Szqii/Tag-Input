<template>
  <div class="tag-container">
    <Tag
      v-for="(tag, index) in tags"
      :key="index"
      :tag="tag"
      :tagColor="color"
      :index="index"
      @removeOneTagEvent="removeOneTag($event)"
    ></Tag>
    <input
      type="text"
      class="input"
      @keydown.enter="addTag"
      @keydown.backspace="removeTag"
    />
    <div class="error" v-if="error">This tag is used before.</div>
  </div>
</template>

<script>
import Tag from "./Tag";
export default {
  components: {
    Tag,
  },
  data() {
    return {
      tags: [],
      error: false,
    };
  },
  methods: {
    addTag(event) {
      let matchedTag = false;
      if (event.target.value.length > 0) {
        this.tags.forEach((tag) => {
          if (tag.toLowerCase() === event.target.value.toLowerCase()) {
            matchedTag = true;
          }
        });
        if (matchedTag) {
          this.error = true;
          setTimeout(() => {
            this.error = false;
          }, 2000);
        } else {
          this.tags.push(event.target.value);
          event.target.value = "";
          this.error = false;
        }
      } else {
        alert("You can not add an empty tag");
      }
    },
    removeTag(event) {
      if (event.target.value <= 0) {
        this.tags.splice(this.tags.length - 1, 1);
      }
    },
    removeOneTag(index) {
      this.tags.splice(index, 1);
    },
  },
  props: {
    value: {
      required: false,
    },
    color: {
      required: false,
      type: String,
      default: "primary",
    },
  },
  created() {
    if (this.value) {
      if (this.value.length > 0) {
        this.tags = this.value.split(",");
      }
    }
  },
  watch: {
    tags() {
      this.$emit("input", this.tags.join(","));
    },
  },
};
</script>

<style lang="scss" scoped>
.tag-container {
  border: 1px solid #ccc;
  padding: 20px;

  .input {
    outline: none;
    height: 30px;
    width: 100px;
    margin-left: 5px;
  }
  .error {
    font-size: 14px;
    color: red;
    margin-top: 5px;
  }
}
</style>
