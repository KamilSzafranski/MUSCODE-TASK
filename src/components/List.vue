<template>
  <Modal
    :products="products"
    :visible="modal"
    @closeModal="handleCloseModal"
    @onEditProduct="handleEditProduct"
  />
  <ul class="mainList">
    <ToDo class="item item-a" />
    <Table class="item item-b" :products="products" />

    <Product
      v-for="product in products"
      class="item"
      :key="product.id"
      :products="product"
      @modalEmit="handleModal"
    />
  </ul>
</template>

<script>
import { nanoid } from "nanoid";
import ToDo from "./ToDo.vue";
import Table from "./Table.vue";
import Product from "./Product.vue";
import Modal from "./Modal.vue";
import img1 from "../assets/img1.png";
import img2 from "../assets/img2.png";
import img3 from "../assets/img3.png";

export default {
  components: {
    ToDo,
    Table,
    Product,
    Modal,
  },
  data() {
    return {
      modal: null,
      products: [
        {
          id: nanoid(),
          name: "iPhone 6s Plus 16GB",
          price: 1000,
          salePrice: 649,
          currency: "$",
          img: [img1],
        },
        {
          id: nanoid(),
          name: "iPad Pro 32GB",
          price: 800,
          salePrice: 600,
          currency: "$",
          img: [img2],
        },
        {
          id: nanoid(),
          name: "MackBook Pro",
          price: 8000,
          salePrice: null,
          currency: "PLN",
          img: [img3],
        },
      ],
    };
  },
  methods: {
    handleModal(id) {
      this.modal = id;
    },

    handleCloseModal() {
      this.modal = null;
    },

    handleEditProduct(product) {
      const productIndex = this.products.findIndex(
        element => element.id == product.id
      );
      console.log(productIndex);
      this.products.splice(productIndex, 1, product);

      this.modal = null;
    },
  },
};
</script>

<style scoped>
.mainList {
  display: grid;
  gap: 10px;
  justify-content: center;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto;
  grid-template-areas:
    "toDo tab tab"
    "firstProduckt secondProduct thirdProduct";
}

.item {
  padding: 20px 10px;
  font-size: 14px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
  border-radius: 5px;
}
.item-a {
  grid-area: toDo;
}
.item-b {
  grid-area: tab;
}
.item-c {
  grid-area: firstProduckt;
}
.item-d {
  grid-area: secondProduct;
}
.item-e {
  grid-area: thirdProduct;
}
</style>
