<template>
  <v-app>
    <v-main>
      <DataTable class="mx-auto my-16" style="width: 80%" />
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
