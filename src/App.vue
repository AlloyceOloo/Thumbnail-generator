<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3 py-5">
        <h1>Generate a thumbnail of a website</h1>
		<img :src="thumbnailUrl"/>
        <form v-on:submit.prevent="makeWebsiteThumbnail">
          <div class="form-group">
            <input v-model="websiteUrl" type="text" id="website-input" placeholder="Enter a website" class="form-control">
          </div>
          <div class="form-group">
            <button class="btn btn-primary">Generate!</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',

  data() { return {
    websiteUrl: '',
    thumbnailUrl: ''
  }  },

  methods: {
    makeWebsiteThumbnail() {
      axios.post("https://shot.screenshotapi.net/screenshot?token={token}&url={url}", {
	token: "7HE9WFB-HNP4EKT-QWPY642-JQXH4FT",
	url: this.websiteUrl,
	width: 1920,
	height: 1000,
	output: 'json',
	thumbnail_width: 300
	})
	.then((response) => {
		this.thumbnailUrl = response.data.screenshot;
	})
	
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
