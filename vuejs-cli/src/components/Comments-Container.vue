<template>
  <div class="container">
    <h1>Comments</h1>
    <hr />
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
    <div class="list-group">
      <div class="list-group-item" v-for="(comment, i) in allComments" :key="i">
        <span class="comment__author"
          >Written by: <strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a v-on:click.prevent="removeComment(i)" href="#" title="Delete"
            >Delete</a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      comments: [
        { name: "João", message: "Lorem ipsum" },
        { name: "Carlos", message: "Lorem ipsum" },
      ],
      name: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      if (this.message.trim() === "") {
        return;
      }
      this.comments.push({ name: this.name, message: this.message });
      this.name = "";
      this.message = "";
    },
    removeComment(i) {
      this.comments.splice(i, 1);
    },
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anonymous" : comment.name,
      }));
    },
  },
  watch: {
    comments(val) {
      console.log("val", val);
    },
  },
};
</script>
