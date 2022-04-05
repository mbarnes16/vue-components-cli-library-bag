<template>
  <b-card-body>
    <b-col md="6">
      <img :src="item.artworkUrl60" alt="Card image" class="mb-3 book">
    </b-col>
    <b-col md="6">
      <b-card-text>
        <h3>{{ item.trackName }}</h3>
        <p>Artist: {{ item.artistName }}</p>
        <div v-if="showExtra">
          <audio :src="item.previewUrl" controls type="audio/x-m4a"></audio>
        </div>
      </b-card-text>
    </b-col>
  </b-card-body>
</template>

<script>
import {MusicVideo} from "@/models/LibraryItems";

export default {
  name: "LibraryMusicVideo",
  props: {
    item: MusicVideo,
    showExtra: {
      type: Boolean,
      default: true,
    }
  },
}
</script>

<style scoped>

</style>