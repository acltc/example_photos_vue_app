<template>
  <div class="container">
    <h1>Edit Photo</h1>
    <form v-on:submit.prevent="updatePhoto(photo)">
      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="photo.name" />
      Width:
      <input type="text" v-model="photo.width" />
      Height:
      <input type="text" v-model="photo.height" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      photo: {},
      errors: []
    };
  },
  created: function() {
    axios.get("/api/photos/" + this.$route.params.id).then(response => {
      this.photo = response.data;
    });
  },
  methods: {
    updatePhoto: function(photo) {
      var params = {
        name: photo.name,
        width: photo.width,
        height: photo.height
      };
      axios
        .patch("/api/photos/" + photo.id, params)
        .then(response => {
          this.$router.push("/photos");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>
