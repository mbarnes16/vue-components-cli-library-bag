<template>
  <div>

    <!--    this is the button to display your cart-->
    //
    <b-button class="float-right" id="show-cart" v-b-modal="'cart-modal'">Cart</b-button>

    <div class="card-columns">
      <library-item
          v-for="item in library"
          :item="item"
          :remove-function="(item) => library.removeItem(item)"
          :add-cart-function="(item) => libraryBag.addToCart(item)"
          :key="item.id">
      </library-item>

      <p>Checked Out: {{ library.checkedOutItems().length }}</p>
    </div>

    <library-bag :model="libraryBag"></library-bag>

  </div>
</template>

<script>
import LibraryCollection from "../models/LibraryCollection";
import {Book, Movie, Album} from "@/models/LibraryItems";
import LibraryItem from "./LibraryItem";
import LibraryBag from "./LibraryBag";
import LibraryBagModel from "../models/LibraryBag";

export default {
  name: "UniversalLibrary",
  components: {
    LibraryItem,
    LibraryBag
  },
  data() {
    return {
      //library: LibraryCollectionDecorator([])
      // or
      library: new LibraryCollection()
          .addItem(new Book('Interaction Design', '', 234))
          .addItem(new Book('Learn Vue', '', 234))
          .addItem(new Movie('The Muppets', '', 187))
          .addItem(new Movie('Strange Brew', '', 97))
          .addItem(new Album('Use Me', 'PVRIS', 16))
          .addItem(new Album('Beautiful Oblivion', 'Issues', 13)),
      //basket: new LibraryCollection(),
      libraryBag: new LibraryBagModel()
      , repairs: new LibraryCollection(),
    }
  },
}
</script>

<style scoped>

</style>