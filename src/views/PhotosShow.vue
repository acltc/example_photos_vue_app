<template>
  <div class="container">
    <h2>{{ photo.name }}</h2>
    <p>Width: {{ photo.width }}</p>
    <p>Height: {{ photo.height }}</p>
    <router-link to="/photos">Back to all photos</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      photo: {}
    };
  },
  created: function() {
    axios.get("/api/photos/" + this.$route.params.id).then(response => {
      this.photo = response.data;
    });
  },
  methods: {}
};
</script>
