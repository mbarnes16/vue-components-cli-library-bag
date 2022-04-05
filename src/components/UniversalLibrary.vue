<template>
  <div>
    <search :add-results-method="addResults" :clear-library-method="clearLibrary"></search>
    <!--    this is the button to display your cart-->
    <b-button class="float-right" id="show-cart" v-b-modal="'cart-modal'">Cart</b-button>
    <p>Checked Out: {{ library.checkedOutItems().length }}</p>

    <div class="card-columns center">
      <library-item
          v-for="item in library"
          :item="item"
          :remove-function="(item) => library.removeItem(item)"
          :add-cart-function="(item) => libraryBag.addToCart(item)"
          :show-cart-message-function="showAlert"
          :key="item.id">
      </library-item>
    </div>
    <library-bag :model="libraryBag"></library-bag>

  </div>
</template>

<script>
import LibraryCollection from "../models/LibraryCollection";
import {Album, Book, Movie, MusicVideo, Song, TVShow} from "@/models/LibraryItems";
import LibraryItem from "./LibraryItem";
import LibraryBag from "./LibraryBag";
import LibraryBagModel from "../models/LibraryBag";
import Search from "../components/Search";

export default {
  name: "UniversalLibrary",
  components: {
    LibraryItem,
    LibraryBag,
    Search,
  },
  data() {
    return {
      //library: LibraryCollectionDecorator([])
      // or
      library: new LibraryCollection()
          .addItem(new Book('', 'Interaction Design', '', '',))
          .addItem(new Book('', 'Learn Vue', '', '',))
          .addItem(new Movie('', 'The Muppets', '', '', '',))
          .addItem(new Movie('', 'Strange Brew', '', '', '',))
          .addItem(new Album('PVRIS', 'Use Me', '', '', '', '',))
          .addItem(new Album('Issues', 'Beautiful Oblivion', '', '', '', '',)),
      //basket: new LibraryCollection(),
      libraryBag: new LibraryBagModel()
      , repairs: new LibraryCollection(),
    }
  },
  methods: {
    addResults(searchResults) {
      for (let i = 0; i < searchResults.length; i++) {
        if (searchResults[i].kind === 'tv-episode') {
          this.library.addItem(Object.assign(new TVShow, searchResults[i]))
        } else if (searchResults[i].kind === 'album') {
          this.library.addItem(Object.assign(new Album, searchResults[i]))
        } else if (searchResults[i].kind === 'music-video') {
          this.library.addItem(Object.assign(new MusicVideo, searchResults[i]))
        } else if (searchResults[i].kind === 'song') {
          this.library.addItem(Object.assign(new Song, searchResults[i]))
        } else if (searchResults[i].kind === 'feature-movie') {
          this.library.addItem(Object.assign(new Movie, searchResults[i]))
        } else if (searchResults[i].kind === 'book' || searchResults[i].kind === 'ebook') {
          this.library.addItem(Object.assign(new Book, searchResults[i]))
        }
      }
    },
    clearLibrary() {
      this.library.splice(0);
    }
  }
}
</script>

<style scoped>

</style>