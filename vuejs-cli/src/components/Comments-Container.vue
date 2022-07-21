<template>
  <div class="container">
    <h1>Comments</h1>
    <FormTodo v-on:addTodo="addComment"></FormTodo>
    <hr />
    <div class="list-group">
      <p v-if="comments.length === 0">No comments yet.</p>
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
import FormTodo from "./Form-Todo";
export default {
  components: {
    FormTodo,
  },
  data() {
    return {
      comments: [
        { name: "João", message: "Lorem ipsum" },
        { name: "Carlos", message: "Lorem ipsum" },
      ],
    };
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
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
