<template>
  <div class="form-todo form-group">
    <p>
      <input
        placeholder="Name"
        type="text"
        name="author"
        class="form-control"
        v-model="name"
      />
    </p>
    <p>
      <textarea
        v-model="message"
        placeholder="Comment"
        name="message"
        class="form-control"
      ></textarea>
    </p>
    <button v-on:click="addComment" type="submit" class="btn btn-primary">
      Comment
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      if (this.message.trim() === "") {
        return;
      }

      this.$emit("addTodo", {
        name: this.name,
        message: this.message,
      });

      this.name = "";
      this.message = "";
    },
  },
};
</script>
