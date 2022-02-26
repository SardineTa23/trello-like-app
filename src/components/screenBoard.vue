<template>
  <div>
    <header>Trello Like App</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <!-- v-bind(:hoge)でバインドさせたコンポーネントにデータを受け渡すことができる -->
        <task-list
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
        />
        <task-list-add />
      </div>
    </main>
  </div>
</template>

<script>
import TaskListAdd from "./TaskListAdd.vue";
import TaskList from "./TaskList";
import { mapState } from "vuex";

export default {
  components: {
    TaskListAdd,
    TaskList,
  },
  computed: {
    ...mapState([
      // stateのlistsを参照
      "lists",
    ]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    },
  },
};
</script>
