<template>
  <v-app>
    <v-main :class="`${$vuetify.theme.dark ? 'grey darken-3' : 'grey lighten-2'}`">
      <v-card class="ma-sm-10">
        <v-card-title class="d-flex justify-space-around">
          <h3 class="mr-sm-16">Country Data</h3>
          <v-switch
            class="order-sm-last ml-sm-16"
            v-model="$vuetify.theme.dark"
            :label="`${$vuetify.theme.dark ? 'Dark Mode' : 'Light Mode'}`"
          ></v-switch>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
            class="flex-shrink-1"
            style="max-width: 600px"
          ></v-text-field>
        </v-card-title>
        <v-data-table
          class="d-flex flex-column"
          show-expand
          single-expand
          item-key="name"
          :expanded.sync="expanded"
          :headers="headers"
          :items="countries"
          :search="search"
        >
          <template v-slot:expanded-item>
            <td colspan="12" style="overflow: hidden; padding: 0; max-width: 95vw">
              <NewsTicker :expandedCountry="getCountry()" />
            </td>
          </template>
          <template v-slot:item.flag="{ item }">
            <div>
              <v-img
                :src="item.flag"
                :alt="item.name"
                height="40px"
                width="60px"
                class="my-1 rounded-lg elevation-2"
              ></v-img>
            </div>
          </template>
          <template v-slot:item.population="{ item }">
            <div>{{parseFloat(item.population).toLocaleString("en")}}</div>
          </template>
        </v-data-table>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
import NewsTicker from "./components/NewsTicker";

export default {
  name: "App",
  data() {
    return {
      search: "",
      expanded: "",
      headers: [
        {
          text: "Country Name (expand for News)",
          align: "start",
          filterable: true,
          value: "name",
          width: "18.5%",
        },
        { text: "Flag", value: "flag" },
        { text: "Region", value: "region" },
        { text: "Sub-region", value: "subregion" },
        { text: "Capital City", value: "capital" },
        { text: "Population", value: "population" },
        { text: "Currency", value: "currencies[0].name" },
        { text: "Language", value: "languages[0].name" },
        { text: "Second Language", value: "languages[1].name" },
      ],
      countries: [],
    };
  },
  methods: {
    getCountry() {
      return this.expanded ? this.expanded[0].name : "Afghanistan";
    },
  },
  components: {
    NewsTicker,
  },
  mounted: function () {
    fetch("https://restcountries.eu/rest/v2/all", {
      method: "get",
    })
      .then((res) => res.json())
      .then((data) => (this.countries = data));
  },
};
</script>