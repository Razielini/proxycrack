<template>
  <v-app-bar
    color="max-height"
    dark
    dense
  >
    <v-toolbar-title>Proxycrack</v-toolbar-title>

    <v-spacer />
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
