<template>
  <div>
    <b-form @submit.prevent="searchMedia()">
      <b-row align="center" style="padding: 20px">
        <b-form-input v-model="searchTerm" class="mr-sm-2" placeholder="Search ITunes" size="sm"
                      style="width: 25%" type="text"></b-form-input>
        <b-button class="my-2 my-sm-0" size="sm" style="width: 5%; padding: 10px" type="submit">Submit</b-button>
      </b-row>
    </b-form>
    <b-row v-if="searching" class="justify-content-sm-center my-4">
      <b-col sm="6">
        <b-alert show variant="warning">Searching...</b-alert>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import axios from "axios";
import LibraryCollection from "../models/LibraryCollection";

export default {
  name: "LibrarySearch",
  data() {
    return {
      searchTerm: '',
      searching: false,
    }
  },
  props: {
    addResultsMethod: Function,
    clearLibraryMethod: Function,
  },
  methods: {
    searchMedia() {
      if (this.searchTerm) {
        // clear results
        this.searchResults = new LibraryCollection();
        this.clearLibraryMethod();
        // display message
        this.searching = true;
        let url = 'https://itunes.apple.com/search';
        let config = {
          params: {
            term: this.searchTerm,
            // sets page limit
            limit: 25,
          },
        }
        // execute ajax request with promises
        axios.get(url, config)
            .then((response) => {
              console.log('AJAX RESPONSE', response);
              this.searchResults = response.data.results;
            })
            .catch((error) => {
              console.error('AJAX ERROR', error.message);
            })
            .finally(() => {
              // hide the searching message
              this.searching = false;
              this.addResultsMethod(this.searchResults);
            })
      }
    },
  }
}
</script>

<style scoped>
</style>