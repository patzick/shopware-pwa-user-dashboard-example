<template>
  <section class="flex flex-col bg-white rounded-md shadow-lg m-2">
    <div class="text-indigo-500 flex flex-col justify-between">
      <img
        :src="getProductThumbnailUrl(product)"
        alt=""
        style="width: 400px; height: auto; max-height: 300px"
      />
    </div>
    <div class="text-indigo-500 px-5 flex flex-col h-full">
      <small class="uppercase mt-2">BEAUTY</small>
      <h3 class="uppercase text-black text-2xl font-medium">
        {{ getProductName({ product }) }}
      </h3>
      <h3 class="text-2xl font-semibold pb-10">
        {{ formatPrice(getProductCalculatedListingPrice(product)) }}
      </h3>
      <div class="flex flex-grow"></div>
      <div class="flex justify-end pb-4">
        <button
          id="addToCartButton"
          class="
            bg-indigo-600
            hover:bg-indigo-500
            focus:outline-none
            transition
            text-white
            uppercase
            px-8
            py-3
          "
          @click="addToCart"
        >
          add
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import { defineComponent } from "@vue/composition-api"
import { useAddToCart } from "@shopware-pwa/composables"
import {
  getProductName,
  getProductCalculatedListingPrice,
  getProductThumbnailUrl,
} from "@shopware-pwa/helpers"
import { usePriceFilter } from "@/logic/usePriceFilter.js"

export default defineComponent({
  props: {
    product: {
      type: Object,
      default: null,
    },
  },
  setup(props) {
    const { addToCart } = useAddToCart({ product: props.product })

    return {
      getProductName,
      getProductCalculatedListingPrice,
      getProductThumbnailUrl,
      formatPrice: usePriceFilter(),
      addToCart,
    }
  },
})
</script>
