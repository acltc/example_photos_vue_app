<template>
  <div class="container">
    <h2>{{ photo.name }}</h2>
    <p>Width: {{ photo.width }}</p>
    <p>Height: {{ photo.height }}</p>
    <button v-on:click="destroyPhoto(photo)">Destroy photo</button>
    <router-link v-bind:to="`/photos/${photo.id}/edit`">Edit photo</router-link>
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
  methods: {
    destroyPhoto: function(photo) {
      axios.delete("/api/photos/" + photo.id).then(response => {
        this.$router.push("/photos");
      });
    }
  }
};
</script>
