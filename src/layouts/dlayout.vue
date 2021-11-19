<template>
  <div class="flex h-screen bg-gray-100 font-sans" v-if="isLoggedIn">
    <div class="flex flex-row flex-wrap flex-1 flex-grow content-start">
      <div class="h-40 lg:h-20 w-full flex flex-wrap">
        <nav
          id="header"
          class="
            bg-white
            w-full
            lg:max-w-sm
            flex
            items-center
            border-b-1 border-gray-300
            order-2
            lg:order-1
          "
        >
          <div class="px-2 w-full"></div>
        </nav>
        <nav
          id="header1"
          class="
            bg-gray-100
            w-auto
            flex-1
            border-b-1 border-gray-300
            order-1
            lg:order-2
          "
        >
          <div class="flex h-full justify-between items-center">
            <!--Search-->
            <div class="relative w-full max-w-3xl px-6"></div>
            <!-- / Search-->

            <!--Menu-->

            <div class="flex relative inline-block pr-6">
              <div class="relative text-sm">
                <button
                  id="userButton"
                  class="flex items-center focus:outline-none mr-3"
                >
                  <img
                    class="w-8 h-8 rounded-full mr-4"
                    src="http://i.pravatar.cc/300"
                    alt="Avatar of User"
                  />
                  <span class="hidden md:inline-block"
                    >Hi, {{ user.firstName }}
                  </span>
                  <svg
                    class="pl-2 h-2"
                    version="1.1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 129 129"
                    xmlns:xlink="http://www.w3.org/1999/xlink"
                    enable-background="new 0 0 129 129"
                  >
                    <g>
                      <path
                        d="m121.3,34.6c-1.6-1.6-4.2-1.6-5.8,0l-51,51.1-51.1-51.1c-1.6-1.6-4.2-1.6-5.8,0-1.6,1.6-1.6,4.2 0,5.8l53.9,53.9c0.8,0.8 1.8,1.2 2.9,1.2 1,0 2.1-0.4 2.9-1.2l53.9-53.9c1.7-1.6 1.7-4.2 0.1-5.8z"
                      ></path>
                    </g>
                  </svg>
                </button>
                <div
                  id="userMenu"
                  class="
                    bg-white
                    nunito
                    rounded
                    shadow-md
                    mt-2
                    absolute
                    mt-12
                    top-0
                    right-0
                    min-w-full
                    overflow-auto
                    z-30
                    invisible
                  "
                >
                  <ul class="list-reset">
                    <li>
                      <a
                        href="#"
                        class="
                          px-4
                          py-2
                          block
                          text-gray-900
                          hover:bg-indigo-400 hover:text-white
                          no-underline
                          hover:no-underline
                        "
                        >My account</a
                      >
                    </li>
                    <li>
                      <a
                        href="#"
                        class="
                          px-4
                          py-2
                          block
                          text-gray-900
                          hover:bg-indigo-400 hover:text-white
                          no-underline
                          hover:no-underline
                        "
                        >Notifications</a
                      >
                    </li>
                    <li>
                      <hr class="border-t mx-2 border-gray-400" />
                    </li>
                    <li>
                      <a
                        href="#"
                        class="
                          px-4
                          py-2
                          block
                          text-gray-900
                          hover:bg-indigo-400 hover:text-white
                          no-underline
                          hover:no-underline
                        "
                        >Logout</a
                      >
                    </li>
                  </ul>
                </div>
              </div>
            </div>

            <!-- / Menu -->
          </div>
        </nav>
      </div>

      <!--Dash Content -->
      <div
        id="dash-content"
        class="
          bg-white
          py-6
          lg:py-0
          w-full
          lg:max-w-sm
          flex flex-wrap
          content-start
        "
      >
        <div class="w-1/2 lg:w-full">
          <div
            class="
              border-2 border-gray-400 border-dashed
              hover:border-transparent hover:bg-white hover:shadow-xl
              rounded
              p-6
              m-2
              md:mx-10 md:my-6
              bg-white
            "
          >
            <div class="flex flex-col items-center">
              <div class="flex-shrink pr-4">
                <div class="rounded-full p-3 bg-indigo-600">
                  <i class="fa fa-wallet fa-fw fa-inverse text-indigo-500"></i>
                </div>
              </div>
              <div class="flex-1 text-center">
                <h3 class="font-bold text-3xl">
                  {{ filterPrice(totalOrdersAmount) }}
                  <span class="text-green-500"
                    ><i class="fas fa-caret-up"></i
                  ></span>
                </h3>
                <h5 class="font-bold text-gray-500">Total Spend</h5>
              </div>
            </div>
          </div>
        </div>

        <div class="w-1/2 lg:w-full">
          <div
            class="
              border-2 border-gray-400 border-dashed
              hover:border-transparent hover:bg-white hover:shadow-xl
              rounded
              p-6
              m-2
              md:mx-10 md:my-6
              bg-white
            "
          >
            <div class="flex flex-col items-center">
              <div class="flex-shrink pr-4">
                <div class="rounded-full p-3 bg-indigo-600">
                  <i class="fas fa-users fa-fw fa-inverse text-indigo-500"></i>
                </div>
              </div>
              <div class="flex-1 text-center">
                <h3 class="font-bold text-3xl">
                  {{ totalOrdersCount }}
                  <span class="text-orange-500"
                    ><i class="fas fa-exchange-alt"></i
                  ></span>
                </h3>
                <h5 class="font-bold text-gray-500">Total Orders</h5>
              </div>
            </div>
          </div>
        </div>

        <div class="w-1/2 lg:w-full">
          <div
            class="
              border-2 border-gray-400 border-dashed
              hover:border-transparent hover:bg-white hover:shadow-xl
              rounded
              p-6
              m-2
              md:mx-10 md:my-6
              bg-white
            "
          >
            <div class="flex flex-col items-center">
              <div class="flex-shrink pr-4">
                <div class="rounded-full p-3 bg-indigo-600">
                  <i
                    class="fas fa-user-plus fa-fw fa-inverse text-indigo-500"
                  ></i>
                </div>
              </div>
              <div class="flex-1 text-center">
                <h3 class="font-bold text-3xl">
                  {{ cartCount }}
                </h3>
                <h5 class="font-bold text-gray-500">Current cart items</h5>
              </div>
            </div>
          </div>
        </div>

        <div class="w-1/2 lg:w-full">
          <div
            class="
              border-2 border-gray-400 border-dashed
              hover:border-transparent hover:bg-white hover:shadow-xl
              rounded
              p-6
              m-2
              md:mx-10 md:my-6
              bg-white
            "
          >
            <div class="flex flex-col items-center">
              <div class="flex-shrink pr-4">
                <div class="rounded-full p-3 bg-indigo-600">
                  <i
                    class="fas fa-user-plus fa-fw fa-inverse text-indigo-500"
                  ></i>
                </div>
              </div>
              <div class="flex-1 text-center">
                <h3 class="font-bold text-3xl"> {{ totalOrderedItems }} </h3>
                <h5 class="font-bold text-gray-500">Total items</h5>
              </div>
            </div>
          </div>
        </div>

        <div class="w-1/2 lg:w-full">
          <div
            class="
              border-2 border-gray-400 border-dashed
              hover:border-transparent hover:bg-white hover:shadow-xl
              rounded
              p-6
              m-2
              md:mx-10 md:my-6
              bg-white
            "
          >
            <div class="flex flex-col items-center">
              <div class="flex-shrink pr-4">
                <div class="rounded-full p-3 bg-indigo-600">
                  <i class="fas fa-server fa-fw fa-inverse text-indigo-500"></i>
                </div>
              </div>
              <div class="flex-1 text-center">
                <h3 class="font-bold text-3xl">{{ lastOrderTime }} </h3>
                <h5 class="font-bold text-gray-500">Last order</h5>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!--Graph Content -->
      <div id="main-content" class="w-full flex-1">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, defineComponent, onMounted, ref } from "@vue/composition-api"
import {
  useUser,
  getApplicationContext,
  useCart,
  useSharedState,
} from "@shopware-pwa/composables"
import { getCustomerOrders } from "@shopware-pwa/shopware-6-client"
import { usePriceFilter } from "@/logic/usePriceFilter.js"
import dayjs from "dayjs"
import relativeTime from "dayjs/plugin/relativeTime"
dayjs.extend(relativeTime)

export default defineComponent({
  setup() {
    const { user, isLoggedIn } = useUser()
    const {sharedRef} = useSharedState()
    const { apiInstance } = getApplicationContext()

    const orders = sharedRef('dashboard-orders', [])

    async function loadOrders() {
      orders.value = await getCustomerOrders(
        {
          sort: "-createdAt",
          associations: { lineItems: {} },
          includes: {
            order: [
              "id",
              "orderNumber",
              "lineItems",
              "amountTotal",
              "orderDateTime",
              "stateMachineState",
              "translated",
            ],
            state_machine_state: ["id", "technicalName", "name", "translated"],
          },
        },
        apiInstance
      )
    }

    onMounted(() => {
      loadOrders()
    })

    const { count: cartCount } = useCart()

    const totalOrdersCount = computed(() => {
      return orders.value.length
    })

    const totalOrdersAmount = computed(() => {
      return orders.value.reduce((acc, order) => {
        return acc + order.amountTotal
      }, 0)
    })

    const totalOrderedItems = computed(() => {
      return orders.value.reduce((acc, order) => {
        return acc + order.lineItems.reduce((acc, lineItem) => {
          return acc + lineItem.quantity
        }, 0)
      }, 0)
    })

    const lastOrderTime = computed(() => {
      const lastOrder = orders.value?.[0]
      return lastOrder && dayjs(lastOrder.orderDateTime).fromNow()
    })

    return {
      isLoggedIn,
      user,
      orders,
      cartCount,
      totalOrdersCount,
      totalOrdersAmount,
      filterPrice: usePriceFilter(),
      totalOrderedItems,
      lastOrderTime
    }
  },
})
</script>

<style scoped>
@import "https://use.fontawesome.com/releases/v5.3.1/css/all.css";
</style>
