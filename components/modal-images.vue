<template>
  <div
    v-if="show"
    class="modal pointer-events-none absolute w-full h-full top-0 left-0 flex items-center justify-center"
  >
    <div
      class="modal-overlay absolute w-full h-full bg-black opacity-25 top-0 left-0 cursor-pointer"
    />
    <div
      class="absolute w-3/4 h-32 bg-white rounded-sm shadow-lg flex items-center justify-center text-2xl"
    >
      🚀
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
  mounted () {
    console.info('mounted :: modal-images')
  }
}
</script>
