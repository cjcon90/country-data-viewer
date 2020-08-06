<template>
  <div>
    <v-sheet class="mx-auto" elevation="8">
      <v-slide-group
        v-model="model"
        class="pa-4"
        :prev-icon="prevIcon ? 'mdi-minus' : undefined"
        :next-icon="nextIcon ? 'mdi-plus' : undefined"
        :multiple="multiple"
        :mandatory="mandatory"
        :show-arrows="showArrows"
        :center-active="centerActive"
      >
        <v-slide-item v-for="n in 15" :key="n" v-slot:default="{ active, toggle }">
          <v-card color="grey lighten-4" class="ma-4" height="200" width="400" @click="toggle">
            <v-row class="fill-height" align="center" justify="center">
              <v-scale-transition>
                <v-icon v-if="active" color="white" size="48" v-text="'mdi-close-circle-outline'"></v-icon>
              </v-scale-transition>
            </v-row>
          </v-card>
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
    country: "American Samoa",
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
      .then((data) => console.log(data.articles));
  },
};
</script>