<template>
  <v-container>
    <h1>TODO LIST</h1>
    <p>ALL: {{todoList.length}} , DONE:{{countDone}} , REMINED:{{todoList.length - countDone}}</p>
    <v-layout row wrap>
      <v-flex xs6 pa-2>
        <List :todoList="todoList" @statusControl="statusControl" @listDelete="listDelete"></List>
      </v-flex>
      <v-flex xs6 pa-2>
        <ListAdd @listAdd="listAdd" @listEdit="listEdit"></ListAdd>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import List from "./List";
import ListAdd from "./ListAdd";

export default {
  components: {
    List,
    ListAdd
  },
  data() {
    return {
      todoList: []
    };
  },
  computed: {
    countDone() {
      let count = 0;
      this.todoList.forEach(list => {
        if (list.status === "done") count++;
      });
      return count;
    }
  },
  methods: {
    listAdd(memo) {
      console.log("receive todolist");
      this.todoList.push({ memo: memo, status: "created" });
    },
    listEdit(memo, index) {
      this.todoList[index].memo = memo;
    },
    statusControl(index, status) {
      console.log("receive btn status");
      this.todoList[index].status = status;
    },
    listDelete(index) {
      this.todoList.splice(index, 1);
    }
  }
};
</script>
