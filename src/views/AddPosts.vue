<template>
  <div class="add-posts">
    <div class="row mb-3">
      <div class="col text-right">
        <button class="btn btn-primary" @click="formshow">Create New Post</button>
      </div>
    </div>
    <div class="card bg-dark mb-3" v-if="formDiv">
      <div class="card-body">
        <form @submit.prevent="addpost">
          <div class="form-group">
            <label>Post Title</label>
            <input
              v-model="title"
              type="text"
              name="title"
              class="form-control"
              placeholder="Enter Post Title"
            />
          </div>
          <div class="form-group">
            <label>Post Detail</label>
            <textarea
              v-model="body"
              name="Body"
              class="form-control"
              placeholder="Enter Post Detail"
            ></textarea>
          </div>
          <div class="row">
            <div class="col-6 mx-auto">
              <button class="btn btn-block btn-success">Create Post</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddPosts",
  data() {
    return {
      formDiv: false,
      titie: "",
      body: "",
    };
  },
  methods: {
    formshow() {
      this.formDiv = true;
    },
    addpost() {
      const newpost = {
        title: this.title,
        body: this.body,
      };
      this.$emit("add-post", newpost);
      (this.title = ""), (this.body = "");
    },
  },
};
</script>

<style scoped>
</style>