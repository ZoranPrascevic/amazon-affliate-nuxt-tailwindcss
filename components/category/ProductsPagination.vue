<template>
  <div id="products-pagination" class="bg-tb-primary rounded p-4 xl:p-6">
    <div class="grid grid-cols-3 gap-4 xl:gap-6">
      <ProductCard
        v-for="(item, index) in paginationData.products"
        :key="JSON.stringify(item)"
        :item="item"
        @hoverstart="setHoverIndex(index)"
        @hoverend="hoveringIndex = 9999"
        class="transition duration-200 hover:tb-shadow-1 bg-white hover:z-10 rounded"
      />
    </div>
    <client-only>
      <paginate
        v-model="paginationData.pageNumber"
        :page-count="paginationData.totalPages"
        :page-range="5"
        :page-link-class="'text-xl w-8 mx-px text-center outline-none'"
        :margin-pages="0"
        :prev-link-class="
          'mr-5 product-pagination-arrow product-pagination-prev outline-none transform rotate-180' +
          (paginationData.totalPages < 6 ? ' hidden' : '')
        "
        :next-link-class="
          'ml-5 product-pagination-arrow product-pagination-next outline-none' +
          (paginationData.totalPages < 6 ? ' hidden' : '')
        "
        :active-class="'text-tb-blue'"
        :disabled-class="'invisible'"
        :break-view-link-class="'hidden'"
        :no-li-surround="true"
        :click-handler="myCallback"
        :prev-text="''"
        :next-text="''"
        :container-class="'flex justify-center items-center text-tb-primary-dark'"
        class="mt-5"
      ></paginate>
    </client-only>
  </div>
</template>

<script>
import ProductCard from "@/components/widget/ProductCard";

export default {
  name: "ProductsPagination",
  components: {
    ProductCard,
  },
  props: ["pageData"],
  data() {
    return {
      paginationData: this.pageData,
      hoveringIndex: 9999,
    };
  },
  methods: {
    setHoverIndex(index) {
      this.hoveringIndex = index;
    },
    myCallback(pageNum) {
      this.$emit("change-page-number", pageNum);
    },
  },
  updated() {
    var paginateNavPrev = this.$el.querySelector(".product-pagination-prev");
    if (paginateNavPrev != null) {
      paginateNavPrev.innerHTML = `<svg width="40" height="40" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="10" cy="10" r="10" fill="#3099F2" />
                    <path
                        d="M12.3913 9.83733L12.3913 9.83733C12.5434 9.9895 12.5434 10.2362 12.3913 10.3883L12.3913 10.3884L9.51514 13.2645L9.51514 13.2645C9.36297 13.4166 9.1163 13.4166 8.96413 13.2645L8.96411 13.2645C8.81196 13.1123 8.81196 12.8656 8.96411 12.7134L8.96411 12.7134L11.5647 10.1128L8.96411 7.51224L8.96228 7.51041L8.96229 7.51039C8.81643 7.35939 8.81644 7.11998 8.96228 6.96897L12.3913 9.83733ZM12.3913 9.83733L9.51514 6.96121L9.51516 6.96119M12.3913 9.83733L9.51516 6.96119M9.51516 6.96119L9.51328 6.95938M9.51516 6.96119L9.51328 6.95938M9.51328 6.95938C9.35848 6.80988 9.11179 6.81417 8.96229 6.96897L9.51328 6.95938Z"
                        fill="white"
                        stroke="white"
                        stroke-width="0.3"
                    />
                </svg>`;
    }
    var paginateNavNext = this.$el.querySelector(".product-pagination-next");
    if (paginateNavNext != null) {
      paginateNavNext.innerHTML = `<svg width="40" height="40" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
				<circle cx="10" cy="10" r="10" fill="#3099F2" />
				<path
					d="M12.3913 9.83733L12.3913 9.83733C12.5434 9.9895 12.5434 10.2362 12.3913 10.3883L12.3913 10.3884L9.51514 13.2645L9.51514 13.2645C9.36297 13.4166 9.1163 13.4166 8.96413 13.2645L8.96411 13.2645C8.81196 13.1123 8.81196 12.8656 8.96411 12.7134L8.96411 12.7134L11.5647 10.1128L8.96411 7.51224L8.96228 7.51041L8.96229 7.51039C8.81643 7.35939 8.81644 7.11998 8.96228 6.96897L12.3913 9.83733ZM12.3913 9.83733L9.51514 6.96121L9.51516 6.96119M12.3913 9.83733L9.51516 6.96119M9.51516 6.96119L9.51328 6.95938M9.51516 6.96119L9.51328 6.95938M9.51328 6.95938C9.35848 6.80988 9.11179 6.81417 8.96229 6.96897L9.51328 6.95938Z"
					fill="white"
					stroke="white"
					stroke-width="0.3"
				/>
			</svg>`;
    }
  },
};
</script>

<style>
</style>