<template>
  <div>
    <v-card
      class="pa-3 mb-3"
      :class="{'done' : list.status === 'done'}"
      v-for="(list, index) in todoList"
      :key="index"
    >
      <p>{{list.memo}}</p>
      <v-btn
        v-if="list.status === 'created'"
        @click="$emit('statusControl', index, 'done')"
        fab
        small
        color="green"
      >완료</v-btn>
      <v-btn v-else fab small color="blue" @click="$emit('statusControl', index, 'created')">취소</v-btn>
      <v-btn @click="$emit('listDelete', index)" fab small color="red">제거</v-btn>
      <v-btn
        @click="listEdit(list.memo, index)"
        v-if="list.status === 'created'"
        fab
        small
        color="yellow"
      >수정</v-btn>
    </v-card>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  props: ["todoList"],
  methods: {
    listEdit(memo, index) {
      eventBus.listEdit(memo, index);
    }
  }
};
</script>

<style scoped>
.done {
  background-color: rgba(0, 0, 0, 0.1);
}
.done p {
  text-decoration: line-through;
  color: rgba(0, 0, 0, 0.5);
}
</style>