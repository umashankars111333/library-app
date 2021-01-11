<template>
  <div class="Books">
    <div class="ml-20">
      <img src="../assets/NotFound.jpg" width="500px" alt="Not Found.." v-show="notFound()" />
    </div>

    <div class="my-5" v-for="booksCategory in Object.keys(filterProduct)" :key="booksCategory">
      <v-container>
        <p v-if="filterProduct[booksCategory].length > 0" class="display-1 font-weight-bold text-capitalize mb-0">{{ booksCategory }}</p>
        <v-layout row wrap class="mt-0">
          <v-flex class="mb-6" xs12 sm5 md4 lg3 v-for="book in filterProduct[booksCategory]" :key="book.title">
            <!-- Books Category -->
            <v-card text class="ma-3" max-width="300">
              <v-img height="250" :src="require(`../assets/books/${booksCategory}/${book.image}`)"></v-img>

              <v-card-title>{{ book.title }}</v-card-title>
              <v-card-text>
                <v-row align="center" class="mx-0">
                  <v-rating :value="4.5" color="amber" dense half-increments readonly size="20"></v-rating>
                </v-row>

                <div class="text-right mt-0">
                  <v-fab-transition>
                    <v-btn fab small dark color="grey">
                      <v-icon color="white">fas fa-plus</v-icon>
                      <!-- <v-icon>mdi-share-variant</v-icon> -->
                    </v-btn>
                  </v-fab-transition>
                </div>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </div>
  </div>
</template>

<script>
export default {
  props: ["filterProduct"],
  data() {
    return {
      notFoundFlag: false,
    };
  },
  methods: {
    notFound() {
      console.log("..boks...", JSON.parse(JSON.stringify(this.filterProduct)));
      Object.keys(this.filterProduct).forEach((booksCategory) => {
        if (this.filterProduct[booksCategory].length > 0) {
          this.notFoundFlag = false;
        } else {
          this.notFoundFlag = true;
        }
      });
      console.log("boolean value", this.notFoundFlag);
      return this.notFoundFlag;
    },
  },
};
</script>

<style>
div.Books {
  clear: both;
}
</style>
