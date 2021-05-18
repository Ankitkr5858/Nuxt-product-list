<template>
  <div class="w-1/2 md:w-1/4 px-2 my-4">
    <div>
      <div class="bg-white rounded-lg shadow-2xl relative">
        <img
          :src="image"
          :alt="name"
          class="rounded-t-lg mx-auto image-loader"
        />
        <div
          class="p-2 absolute bottom-0 text-white bg-opacity-80 bg-black w-full"
        >
          <span class="font-bold text-sm md:text-xl mb-2">
            {{ name }}
          </span>
          <strong class="block text-md md:text-xl">{{ price }} $</strong>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    image: {
      type: String,
      default: '',
    },
    name: {
      type: String,
      default: '',
    },
    price: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {}
  },
}
</script>

<style lang="css">
.image-loader {
  width: 100%;
  min-height: 100px;
  display: inline-block;
  border-radius: 3px;
  animation: 2s linear 0s infinite normal none running image-loader;
  background: linear-gradient(
      to right,
      rgb(239, 241, 243) 4%,
      rgb(226, 226, 226) 25%,
      rgb(239, 241, 243) 36%
    )
    0% 0% / 1000px 100%;
}
@keyframes image-loader {
  0% {
    background-position: -1000px 0px;
  }

  100% {
    background-position: 1000px 0px;
  }
}
</style>
