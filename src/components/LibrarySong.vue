<template>
  <b-card-body>
    <img :src="item.artworkUrl60" alt="Card image" class="mb-3 book">
    <b-card-text>
      <h3>{{ item.trackName }}</h3>
      <p>Artist: {{ item.artistName }}</p>
      <div v-if="showExtra">
        <p>Collection: {{ item.collectionName }}</p>
        <p v-if="item.primaryGenreName">Genre: {{ item.primaryGenreName }}</p>
        <p v-if="item.contentAdvisoryRating">Rating: {{ item.contentAdvisoryRating }}</p>
        <audio :src="item.previewUrl" controls type="audio/x-m4a"></audio>
      </div>
    </b-card-text>

  </b-card-body>
</template>

<script>
import {Song} from "@/models/LibraryItems";

export default {
  name: "LibrarySong",
  props: {
    item: Song,
    showExtra: {
      type: Boolean,
      default: true,
    }
  },
}
</script>

<style scoped>
</style>