<template>
  <div>
    <v-textarea outlined v-model="memo" label="Input TodoList" value></v-textarea>
    <v-btn v-if="mode==='add'" @click="listAdd">ADD</v-btn>
    <v-btn v-else @click="listEdit">EDIT</v-btn>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  components: {},
  methods: {
    listAdd() {
      if (this.memo == null) {
        alert("INPUT TODOLIT");
      } else {
        this.$emit("listAdd", this.memo);
        this.memo = null;
      }
    },
    listEdit() {
      if (this.memo == null) {
        alert("INPUT CONTENTS");
      } else {
        this.$emit("listEdit", this.memo, this.index);
        this.memo = null;
        this.mode = "add";
      }
    }
  },
  created() {
    eventBus.$on("listEdit", (memo, index) => {
      this.memo = memo;
      this.index = index;
      this.mode = "edit";
    });
  },
  data() {
    return {
      memo: null,
      index: null,
      mode: "add"
    };
  }
};
</script>
