<template>
  <b-card-body>
    <img :src="item.artworkUrl60" alt="Card image" class="mb-3 book">
    <b-card-text>
      <h3>{{ item.trackName }}</h3>
      <p>Season: {{ item.collectionName }}</p>
      <div v-if="showExtra">
        <p v-if="item.primaryGenreName">Genre: {{ item.primaryGenreName }}</p>
        <p v-if="item.contentAdvisoryRating">Rating: {{ item.contentAdvisoryRating }}</p>
        <p v-if="item.longDescription">Description: {{ item.longDescription }}</p>
        <audio :src="item.previewUrl" controls type="audio/x-m4a"></audio>
      </div>
    </b-card-text>

  </b-card-body>
</template>

<script>
import {TVShow} from "@/models/LibraryItems";

export default {
  name: "LibraryTVShow",
  props: {
    item: TVShow,
    showExtra: {
      type: Boolean,
      default: true,
    }
  },
}
</script>

<style scoped>
</style>