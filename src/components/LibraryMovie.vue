<template>
  <b-card-body>
    <img :src="item.artworkUrl60" alt="Card image" class="mb-3 book">
    <b-card-text>
      <h3>{{ item.trackName }}</h3>
      <p>Director: {{ item.artistName }}</p>
      <div v-if="showExtra">
        <p v-if="item.longDescription">Description: {{ item.longDescription }}</p>
        <p v-if="item.contentAdvisoryRating">Rating: {{ item.contentAdvisoryRating }}</p>
      </div>
    </b-card-text>
  </b-card-body>
</template>

<script>
import {Movie} from "@/models/LibraryItems";

export default {
  name: "LibraryMovie",
  props: {
    item: Movie,
    showExtra: {
      type: Boolean,
      default: true,
    }
  },
}
</script>

<style scoped>
</style>