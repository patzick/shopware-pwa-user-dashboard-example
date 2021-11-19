<template>
  <div class="flex flex-1 flex-wrap">
    <div class="w-full px-6">
      <!--"Container" for the graphs"-->
      <div class="max-w-full lg:max-w-3xl xl:max-w-5xl">
        <!--Graph Card-->
        <div class="border-b p-3">
          <h5 class="font-bold text-black">Order again (top 3)</h5>
        </div>
        <div class="p-5 bg-gray-100 flex flex-col md:flex-row">
          <OurProductCard
            v-for="product in topProducts"
            :key="product.id"
            :product="product"
          />
        </div>
        <!--/Graph Card-->
      </div>
    </div>
  </div>
</template>

<script>
import { computed, defineComponent, ref, watch } from "@vue/composition-api"
import {
  useSharedState,
  getApplicationContext,
} from "@shopware-pwa/composables"
import { getProducts } from "@shopware-pwa/shopware-6-client"
import OurProductCard from "@/components/OurProductCard.vue"

export default defineComponent({
  layout: "dlayout",
  setup() {
    const { sharedRef } = useSharedState()
    const { apiInstance } = getApplicationContext()
    const orders = sharedRef("dashboard-orders", [])
    const groupLiteItemsByPopularity = computed(() => {
      return orders.value.reduce((acc, order) => {
        order.lineItems.forEach((lineItem) => {
          acc[lineItem.productId] ??= {
            count: 0,
          }
          acc[lineItem.productId].count += lineItem.quantity
        })
        return acc
      }, {})
    })
    const topLineItems = computed(() => {
      return Object.entries(groupLiteItemsByPopularity.value)
        .sort(([, a], [, b]) => b.count - a.count)
        .slice(0, 3)
    })
    const topProducts = ref([])
    async function fetchTopProducts() {
      return await getProducts(
        { ids: topLineItems.value.map(([id]) => id) },
        apiInstance
      )
    }
    watch(topLineItems, async () => {
      const response = await fetchTopProducts()
      topProducts.value = response.elements || []
    })

    return {
      groupLiteItemsByPopularity,
      topLineItems,
      topProducts,
    }
  },
  components: { OurProductCard },
})
</script>
