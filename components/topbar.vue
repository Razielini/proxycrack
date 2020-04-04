<template>
  <v-app-bar
    color="deep-purple accent-4 max-height"
    dark
    dense
  >
    <v-toolbar-title>Proxycrack</v-toolbar-title>

    <v-spacer />

    <v-btn icon>
      <v-icon>mdi-heart</v-icon>
    </v-btn>

    <v-btn icon>
      <v-icon>mdi-magnify</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  mounted () {
    console.info('mounted :: TopBar')
  }
}
</script>

<style>
  .max-height {
    max-height: 48px;
  }
</style>
