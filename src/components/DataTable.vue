<template>
  <v-card>
    <v-card-title class="d-flex justify-space-around">
      <h3 class="mr-sm-16">Country List</h3>
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
      show-expand
      single-expand
      item-key="name"
      :headers="headers"
      :items="countries"
      :search="search"
    >
      <template v-slot:expanded-item="{item}">
        <td :colspan="headers.length">More info about {{ item.name }}</td>
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
    <NewsTicker class="rounded" />
  </v-card>
</template>



<script>
import NewsTicker from "./NewsTicker";

export default {
  name: "DataTable",
  data() {
    return {
      search: "",
      isExpanded: false,
      headers: [
        {
          text: "Country Name",
          align: "start",
          filterable: true,
          value: "name",
          width: "20%",
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
