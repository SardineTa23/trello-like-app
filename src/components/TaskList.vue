<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <!-- computedの呼び出し -->
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <draggable group="cards" :list="cards" @end="$emit('change')">
      <card-show
        v-for="(item, index) in cards"
        :body="item.body"
        :key="item.id"
        :cardIndex="index"
        :listIndex="listIndex"
      />
      <card-add :listIndex="listIndex" />
    </draggable>
  </div>
</template>

<script>
import CardAdd from "./CardAdd";
import CardShow from "./CardShow";
import draggable from "vuedraggable";

export default {
  components: {
    CardAdd,
    CardShow,
    draggable,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    cards: {
      type: Array,
      required: true,
    },
    listIndex: {
      type: Number,
      required: true,
    },
  },
  computed: {
    totalCardInList() {
      return this.cards.length;
    },
  },
  methods: {
    removeList: function () {
      if (confirm("本当にこのリストを削除しますか？")) {
        this.$store.dispatch("removelist", { listIndex: this.listIndex });
      }
    },
  },
};
</script>
