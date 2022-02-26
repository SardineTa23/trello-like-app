<template>
  <div>
    <header>Trello Like App</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable :list="lists" @end="movingList" class="list-index">
        <!-- v-bind(:hoge)でバインドさせたコンポーネントにデータを受け渡すことができる -->
        <task-list
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
          @change="movingCard"
        />
        <task-list-add />
      </draggable>
    </main>
  </div>
</template>

<script>
import TaskListAdd from "./TaskListAdd.vue";
import TaskList from "./TaskList";
import { mapState } from "vuex";
import draggable from "vuedraggable";

export default {
  components: {
    TaskListAdd,
    TaskList,
    draggable,
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
  methods: {
    movingCard: function () {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingList: function () {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
  },
};
</script>
