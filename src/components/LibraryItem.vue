<template>
  <b-card>
    <component :is="typeOfItem" :item="item"></component>
    <b-card-footer>
      <button class="btn btn-secondary" v-if="item.isAvailable()" @click="item.checkOut()">Check Out</button>
      <button class="btn btn-secondary" v-else @click="item.checkIn()">Check In</button>
      <button class="btn btn-secondary" @click="addCartFunction(item); showCartMessageFunction()">Add to Cart</button>
      <button class="btn btn-danger" @click="removeFunction(item)">Remove</button>
    </b-card-footer>
  </b-card>
</template>

<script>
import Book from "./LibraryBook";
import Movie from "./LibraryMovie";
import Album from "./LibraryAlbum";
import TVShow from "./LibraryTVShow";
import MusicVideo from "./LibraryMusicVideo";
import Song from "./LibrarySong";

export default {
  name: "LibraryItem",
  components: {
    Book,
    Movie,
    Album,
    TVShow,
    MusicVideo,
    Song,
  },
  props: {
    item: Object,
    removeFunction: Function,
    addCartFunction: Function,
    showCartMessageFunction: Function,
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