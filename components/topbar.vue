<template>
  <v-app-bar
    color="deep-purple accent-4"
    dark
    dense
  >
    <v-app-bar-nav-icon />

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
