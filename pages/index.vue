<template>
  <div class="container mx-auto">
    <div
      class="flex md:flex-row flex-col justify-evenly items-center mt-12 mb-3"
    >
      <div class="flex justify-center w-full">
        <div class="relative inline-flex align-center mb-3">
          <label for="" class="m-auto mr-4">Choose a Category</label>
          <svg
            class="w-2 h-2 absolute top-0 right-0 m-4 pointer-events-none"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 412 232"
          >
            <path
              d="M206 171.144L42.678 7.822c-9.763-9.763-25.592-9.763-35.355 0-9.763 9.764-9.763 25.592 0 35.355l181 181c4.88 4.882 11.279 7.323 17.677 7.323s12.796-2.441 17.678-7.322l181-181c9.763-9.764 9.763-25.592 0-35.355-9.763-9.763-25.592-9.763-35.355 0L206 171.144z"
              fill="#648299"
              fill-rule="nonzero"
            />
          </svg>
          <select
            v-model="selectedCategory"
            class="
              border border-gray-300
              rounded-full
              text-gray-600
              h-10
              pl-5
              pr-10
              bg-white
              hover:border-gray-400
              focus:outline-none
              appearance-none
            "
          >
            <option value="">All</option>
            <option v-for="category in categories" :key="category">
              {{ category }}
            </option>
          </select>
        </div>
      </div>
      <div class="flex justify-end text-gray-700 mb-3">
        <button
          :disabled="responseData.current_page == 1"
          class="
            h-8
            w-8
            mr-1
            flex
            justify-center
            items-center
            disabled:opacity-50
            disabled:cursor-not-allowed
          "
          @click="getProductByPage(1)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M15.707 15.707a1 1 0 01-1.414 0l-5-5a1 1 0 010-1.414l5-5a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 010 1.414zm-6 0a1 1 0 01-1.414 0l-5-5a1 1 0 010-1.414l5-5a1 1 0 011.414 1.414L5.414 10l4.293 4.293a1 1 0 010 1.414z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
        <button
          :disabled="responseData.current_page == 1"
          class="
            h-8
            w-8
            mr-1
            flex
            justify-center
            items-center
            disabled:opacity-50
            disabled:cursor-not-allowed
          "
          @click="getProductByPage(responseData.current_page - 1)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
        <div class="flex h-8 font-medium">
          <div
            class="
              w-8
              flex
              justify-center
              items-center
              leading-5
              transition
              duration-150
              ease-in
              border-b-2
            "
          >
            {{ responseData.current_page }}
          </div>
        </div>
        <button
          :disabled="responseData.current_page == responseData.last_page"
          class="
            h-8
            w-8
            ml-1
            flex
            justify-center
            items-center
            disabled:opacity-50
            disabled:cursor-not-allowed
          "
          @click="getProductByPage(responseData.current_page + 1)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
        <button
          :disabled="responseData.current_page == responseData.last_page"
          class="
            h-8
            w-8
            ml-1
            flex
            justify-center
            items-center
            cursor-pointer
            disabled:opacity-50
            disabled:cursor-not-allowed
          "
          @click="getProductByPage(responseData.last_page)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M10.293 15.707a1 1 0 010-1.414L14.586 10l-4.293-4.293a1 1 0 111.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
              clip-rule="evenodd"
            />
            <path
              fill-rule="evenodd"
              d="M4.293 15.707a1 1 0 010-1.414L8.586 10 4.293 5.707a1 1 0 011.414-1.414l5 5a1 1 0 010 1.414l-5 5a1 1 0 01-1.414 0z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
      </div>
    </div>

    <div class="text-center">
      <div class="flex flex-wrap justify-center mx-auto mb-8">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :image="product.image"
          :name="product.name"
          :price="product.price"
        />
      </div>
    </div>
  </div>
</template>
<script>
import ProductCard from '@/components/ProductCard'
export default {
  components: { ProductCard },
  data() {
    return {
      productList: [],
      responseData: {},
      categories: [],
      selectedCategory: '',
    }
  },
  async fetch() {
    this.responseData = await fetch(
      'https://trayvonnorthern.com/Edgewood-API/public/api/products'
    ).then((res) => res.json())
    this.productList = this.responseData.data
    this.categories = [
      ...new Set(this.productList.map((product) => product.catname)),
    ]
  },
  computed: {
    products() {
      return this.productList.filter(
        (product) =>
          !this.selectedCategory || product.catname === this.selectedCategory
      )
    },
  },
  methods: {
    async getProductByPage(pageNumber) {
      this.responseData = await fetch(
        'https://trayvonnorthern.com/Edgewood-API/public/api/products?page=' +
          pageNumber
      ).then((res) => res.json())
      this.productList = this.responseData.data
      this.categories = [
        ...new Set(this.productList.map((product) => product.catname)),
      ]
    },
  },
}
</script>
