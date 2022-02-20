<template>
  <!-- サブミットイベント時にaddListメソッドをハンドル -->
  <!-- @はv-onの省略記法 -->
  <!-- .preventはVueのイベント修飾詞であり、サブミット時にリロードされるのを防ぐ -->
  <form :class="classList" @submit.prevent="addList">
    <input
      v-model="title"
      type="text"
      class="text-input"
      placeholder="Add new list"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <button type="submit" class="add-button" v-if="isEditing || titleExists">
      Add
    </button>
  </form>
</template>

<script>
export default {
  data: function () {
    return {
      title: "",
      isEditing: false,
    };
  },
  computed: {
    // return array
    classList() {
      const classList = ["addlist"];
      if (this.isEditing) {
        classList.push("active");
      }
      if (this.titleExists) {
        classList.push("addable");
      }
      return classList;
    },

    // return bool
    titleExists() {
      return this.title.length > 0;
    },
  },
  methods: {
    addList: function () {
      this.$store.dispatch("addlist", { title: this.title });
      this.title = "";
    },
    startEditing: function () {
      this.isEditing = true;
    },
    finishEditing: function () {
      this.isEditing = false;
    },
  },
};
</script>
