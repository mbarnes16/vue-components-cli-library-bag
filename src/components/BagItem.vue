<template>
  <div class="card">
    <div class="card-body">
      <component :is="typeOfItem" :item="item"></component>
    </div>
    <div class="card-footer">
      <button class="btn btn-danger" @click="removeFromCartFunction(item)">Remove</button>
    </div>
  </div>
</template>

<script>
import Book from "./LibraryBook";
import Movie from "./LibraryMovie";
import Album from "./LibraryAlbum";
import MusicVideo from "./LibraryMusicVideo";
import Song from "./LibrarySong";
import TVShow from "./LibraryTVShow";

export default {
  name: "BagItem",
  components: {
    Book,
    Movie,
    Album,
    MusicVideo,
    Song,
    TVShow,

  },
  props: {
    item: Object,
    removeFromCartFunction: Function,
  },
  computed: {
    typeOfItem() {
      return this.item.constructor.name;
    }
  },
}
</script>

<style scoped>
</style>