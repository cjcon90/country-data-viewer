<template>
  <div>
    <v-sheet class="mx-auto" elevation="8">
      <v-slide-group v-model="model" show-arrows center-active>
        <v-slide-item v-for="story in news" :key="story">
          <a :href="story.url" target="_blank" style="text-decoration: none;">
            <v-card
              color="grey lighten-4"
              class="ma-4"
              height="200"
              width="275"
              :style="{ backgroundImage: 'url(' + story.urlToImage + ')' }"
              style="background-size: cover; max-width: 64vw"
            >
              <h3
                style="width: 100%"
                :class="`${$vuetify.theme.dark ? 'grey darken-4' : 'grey lighten-5'}`"
              >{{story.title}}</h3>
              <h4
                style="position: absolute; bottom: 0; width: 100%"
                :class="`${$vuetify.theme.dark ? 'grey darken-4' : 'grey lighten-5'}`"
              >{{story.author}}</h4>

              <v-row class="fill-height" align="center" justify="center"></v-row>
            </v-card>
          </a>
        </v-slide-item>
      </v-slide-group>
    </v-sheet>
  </div>
</template>

<script>
export default {
  name: "NewsTicker",
  data: () => ({
    model: null,
    multiple: false,
    mandatory: false,
    showArrows: true,
    prevIcon: false,
    nextIcon: false,
    centerActive: false,
    country: "Lebanon",
    news: [],
  }),
  mounted() {
    fetch(
      `https://newsapi.org/v2/everything?q=${this.country}&apiKey=6086863167d54723950f6ab17b77332a`,
      {
        method: "get",
      }
    )
      .then((res) => res.json())
      .then((data) => (this.news = data.articles));
  },
};
</script>