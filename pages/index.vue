<template>
  <div class="h-screen">
    <div
      class="flex justify-center items-center flex-col"
    >
      <h1 class="title">
        proxycrack
      </h1>
      <h2 class="subtitle">
        Create proxy-card of your favorites games
      </h2>
    </div>

    <div
      class="flex justify-around"
    >
      <div>
        Row 1<br>
        Row 1<br>
        Row 1<br>
        Row 1<br>
        Row 1<br>
        Row 1
        Row 1
        Row 1
      </div>

      <div
        id="wrapper-divination-card"
        style="background-image: url(https://gamepedia.cursecdn.com/pathofexile_gamepedia/c/c8/Alone_in_the_Darkness_card_art.png?version=4759af65641ef85601300dd68fc30da2);"
      >
        <div
          id="frame-divination-card"
          class="flex flex-col items-center"
        >
          <div
            class="my-4 text-lg text-divination-title"
          >
            {{ divination.title }}
          </div>
          <div
            class="mx-16 mt-64 self-start text-base text-white"
          >
            {{ divination.stack }}
          </div>
          <div
            class="my-12 text-base text-divination-reward"
          >
            {{ divination.reward }}
          </div>
          <div
            class="max-w-xs text-base text-divination-reward"
          >
            {{ divination.lore }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    divination: {
      title: 'Alone in the Darkness',
      stack: '6',
      reward: 'Delve Item',
      lore: 'Sometimes, the most beautiful treasures...are the ones you cannot have. - Beryl, Survivor from the Azurite Mines'
    }
  })
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/

#frame-divination-card {
  background-image: url('/poe/divination/divination_card_frame.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  min-width: 440px;
  min-height: 668px;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
</style>
