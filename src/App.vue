<template>
  <v-app>
    <v-main :class="`${$vuetify.theme.dark ? 'grey darken-3' : 'grey lighten-2'}`">
      <DataTable class="ma-sm-10" />
    </v-main>
  </v-app>
</template>

<script>
import DataTable from "./components/DataTable";

export default {
  name: "App",

  components: {
    DataTable,
  },

  data: () => ({
    //
  }),
};
</script>
