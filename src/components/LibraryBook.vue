<template>
  <b-card-body>

    <img :src="item.artworkUrl60" alt="Card image" class="mb-3 book">


    <b-card-text>
      <h3>{{ item.trackName }}</h3>
      <p>Author: {{ item.artistName }}</p>
      <div v-if="showExtra">
        <p v-if="item.description">Description: {{ item.description }}</p>
      </div>
    </b-card-text>
  </b-card-body>
</template>

<script>
import {Book} from "@/models/LibraryItems";

export default {
  name: "LibraryBook",
  props: {
    item: Book,
    showExtra: {
      type: Boolean,
      default: true,
    }
  },
}
</script>

<style scoped>
</style>