<template>
  <li class="wrapper" @click="handleModal">
    <h4 class="title">
      {{ products.name }}
    </h4>
    <figure
      class="imgBox"
      :class="{
        sale: !products.salePrice,
      }"
    >
      <div v-if="products.salePrice" class="saleOverlay">
        {{ salePercent }}%
      </div>
      <img class="image" :src="products.img" />
    </figure>
    <figcaption class="imgText">
      <p v-if="products.salePrice" class="salePrice">
        {{ products.salePrice }} {{ products.currency }}
      </p>

      <p
        class="price"
        :class="{
          isSale: products.salePrice,
        }"
      >
        {{ products.price }} {{ products.currency }}
      </p>
    </figcaption>
  </li>
</template>

<script>
import { computed } from "@vue/reactivity";

export default {
  props: ["products"],
  computed: {
    salePercent() {
      const calc =
        ((this.products.price - this.products.salePrice) /
          this.products.price) *
        100;

      return Math.round(calc);
    },
  },
  methods: {
    handleModal() {
      this.$emit("modalEmit", this.products.id);
    },
  },
};
</script>

<style scoped>
.wrapper {
  position: relative;
  overflow: hidden;
  cursor: pointer;
}
.title {
  margin-bottom: 15px;
  color: var(--var-title-color);
}
.image {
  height: 180px;
}
.imgBox {
  margin-bottom: 8px;
  display: flex;
  justify-content: center;
}

.imgText {
  text-align: center;
}

.salePrice {
  margin-bottom: 5px;
  font-weight: 700;
  color: var(--var-btn-color);
}
.isSale {
  text-decoration: line-through;
}

.saleOverlay {
  width: 60%;
  text-align: center;
  right: -70px;
  top: 30px;
  position: absolute;
  background-color: black;
  color: white;
  transform: rotate(45deg);
}

.sale {
  margin-bottom: 28px;
}
</style>
