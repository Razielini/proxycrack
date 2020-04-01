<template>
  <div
    v-if="show"
    class="modal absolute w-full h-full top-0 left-0 flex items-center justify-center"
  >
    <div
      class="modal-overlay absolute w-full h-full bg-black opacity-25 top-0 left-0 pointer-events-none"
    />
    <div
      class="absolute w-3/4 rounded-sm shadow-lg flex items-center justify-start text-2xl items-baseline flex-col bg-gray-900"
    >
      <div
        class="flex justify-between w-full border-solid border-black border-b-2 title-bench px-8 py-2"
      >
        Existing Images
        <input
          class="form-input block w-64 sm:text-sm sm:leading-5 p-2"
          placeholder="Write a Divination Card"
        >
      </div>

      <div
        class="flex-wrap justify-around"
      >
        <div
          v-for="(cardItem, i) in divination_images"
          @click="selectCard(cardItem)"
          :key="'modal-img-' + i"
          class="card-image mx-1 my-2 justify-start border-2 border-solid border-black inline-block cursor-pointer"
        >
          <div
            class="title flex justify-center text-base items-center font-thin"
          >
            {{ cardItem.title }}
          </div>
          <img
            :src="'poe/divination/img/' + cardItem.src"
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    divination_images: [
      {
        title: 'A Dab of Ink',
        src: 'A_Dab_of_Ink_card_art.png'
      },
      {
        title: 'A Mothers Parting Gift',
        src: 'A_Mothers_Parting_Gift_card_art.png'
      },
      {
        title: 'Abandoned Wealth',
        src: 'Abandoned_Wealth_card_art.png'
      },
      {
        title: 'AkilsProphecy',
        src: 'Akils_Prophecy_card_art.png'
      },
      {
        title: 'Alluring Bounty',
        src: 'Alluring_Bounty_card_art.png'
      }
    ]
  }),
  mounted () {
    console.info('mounted :: modal-images')
  },
  methods: {
    selectCard (cardItem) {
      console.log('selectCard :: ', cardItem)
      this.$emit('card', cardItem)
      this.$emit('update:show', false)
    }
  }
}
</script>

<style>
  .card-image {
    width: 200px;
  }

  .card-image img {
    width: 200px;
  }

  .card-image .title {
    height: 34px;
    color: #ffff77;
    background: url(/poe/divination/ui/HeadRareLeft.png) no-repeat left top,
                url(/poe/divination/ui/HeadRareRight.png) no-repeat right top,
                url(/poe/divination/ui/HeadRareLineCenter.png) repeat-x right top;
  }
</style>
