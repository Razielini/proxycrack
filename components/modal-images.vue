<template>
  <div
    v-if="show"
    class="modal absolute w-full left-0 flex items-center justify-center"
    style="height: 50vh;"
  >
    <div
      class="modal-overlay absolute w-full h-full bg-black opacity-25 top-0 left-0 pointer-events-none"
    />
    <div
      class="absolute rounded-sm w-full h-full shadow-lg flex items-center justify-start text-2xl items-baseline flex-col bg-gray-900"
    >
      <div
        class="flex justify-between w-full border-solid border-black border-b-2 title-bench px-8 py-2"
      >
        Existing Images

        <div
          class="flex flex-row"
        >
          <p
            class="mx-2 cursor-pointer"
            @click="lessPage"
          >
            Prev
          </p>
          <label>
            {{ pagination.page }}/{{ totalPages }}
          </label>
          <p
            class="mx-2 cursor-pointer"
            @click="addPage"
          >
            Next
          </p>
        </div>
      </div>

      <div
        class="flex-wrap justify-around"
      >
        <div
          v-for="(cardItem, i) in divinationPaginated()"
          :key="'modal-img-' + i"
          class="card-image px-2 my-2 w-1/2 md:w-1/4 justify-start inline-block cursor-pointer"
          @click="selectCard(cardItem)"
        >
          <div
            class="title flex justify-center text-base items-center font-thin truncate"
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

<script lang="ts">
import { Component, Vue, Prop } from 'nuxt-property-decorator'

@Component
export default class PoeModalImages extends Vue {
  @Prop({ type: Boolean, default: false })
  show: false

  divinationImages: any[] = this.$store.state.poeDivination.images
  pagination: any = {
    page: 1,
    itemsPerPage: 8
  }

  get totalPages () {
    return Math.ceil(Math.trunc(this.divinationImages.length / this.pagination.itemsPerPage))
  }

  mounted () {
    console.info('mounted :: modal-images')
  }

  divinationPaginated () {
    const images = [...this.divinationImages]
    const itemsPerPage: number = this.pagination.itemsPerPage
    const initial: number = ((this.pagination.page - 1) * itemsPerPage)
    console.log('images :: ', images)
    console.log('initial :: ', initial)
    const slice = images.slice(initial, initial + itemsPerPage)
    console.log('slice :: ', slice)
    return images.slice(initial, initial + itemsPerPage)
  }

  selectCard (cardItem: any) {
    console.log('selectCard :: ', cardItem)
    this.$emit('card', cardItem)
    this.$emit('update:show', false)
  }

  addPage () {
    this.pagination.page++
    if (this.pagination.page > this.totalPages) {
      this.pagination.page = 1
    }
  }

  lessPage () {
    this.pagination.page--
    if (this.pagination.page <= 0) {
      this.pagination.page = this.totalPages
    }
  }
}
</script>

<style>
  .card-image {
    filter: grayscale(100%);
  }

  .card-image:hover {
    filter: grayscale(0%);
  }

  .card-image img {
  }

  .card-image .title {
    height: 34px;
    color: #ffff77;
    background: url(/poe/divination/ui/HeadRareLeft.png) no-repeat left top,
                url(/poe/divination/ui/HeadRareRight.png) no-repeat right top,
                url(/poe/divination/ui/HeadRareLineCenter.png) repeat-x right top;
  }
</style>
