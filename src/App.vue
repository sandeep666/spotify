<template>
  <div id="app">
    <export-excel :data="items">
      Download Data
    </export-excel>
    <b-table striped hover :items="items"></b-table>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import { AudioData } from "../../audioData";
import { PlaylistData } from "../../playlistData";
export default {
  name: "App",
  components: {
    HelloWorld
  },
  computed: {
    items: function() {
      return PlaylistData.map(data => {
        let trackId = data.track.id;
        const audioFeature = AudioData.filter(data => data.id === trackId);
        console.log(data.track, audioFeature[0]);
        const Album = data.track.name;
        const Artists = data.track.artists.map(data => data.name).flat();
        const trackInfo = {
          Artists,
          Album,
          ...audioFeature[0]
        };
        return trackInfo;
      });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
