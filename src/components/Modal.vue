<template>
  <div v-if="visible" class="modalBackdrop">
    <div class="modal">
      <h3 class="title">Edycja produktu: iPhone 6s Plus 16GB</h3>
      <img :src="dataToRender[0].img" class="img" />
      <form class="productForm" @submit="onSubmit" id="modalForm">
        <Label class="formLabel">
          Nazwa produktu

          <input
            class="formInput"
            type="text"
            name="name"
            :value="dataToRender[0].name"
          />
        </Label>
        <Label class="formLabel">
          Cena
          <input
            class="formInput"
            type="number"
            name="price"
            :value="dataToRender[0].price"
          />
        </Label>
        <Label class="formLabel" type="text" name="salePrice">
          Promocyjna cena
          <input
            class="formInput"
            type="number"
            name="salePrice"
            :value="dataToRender[0].salePrice"
          />
        </Label>
        <Label class="formLabel">
          Waluta
          <select name="currency" class="formSelect">
            <option value="$" :selected="dataToRender[0].currency === `$`">
              $
            </option>
            <option value="PLN" :selected="dataToRender[0].currency === `PLN`">
              PLN
            </option>
            <option value="EUR" :selected="dataToRender[0].currency === `EUR`">
              EUR
            </option>
          </select>
        </Label>
      </form>

      <div class="modalBtnBox">
        <button type="submit" class="submitBtn" form="modalForm">Zapisz</button>
        <button type="button" class="btn" @click="onCloseModal">Anuluj</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["products", "visible"],
  computed: {
    dataToRender() {
      const modalData = this.products.filter(
        element => element.id === this.visible
      );

      return modalData;
    },
  },

  methods: {
    onCloseModal() {
      this.$emit("closeModal");
    },

    onSubmit(event) {
      event.preventDefault();
      const { name, price, salePrice, currency } = event.currentTarget.elements;

      const editedProduct = {
        img: this.dataToRender[0].img,
        id: this.dataToRender[0].id,
        name: name.value,
        price: price.value,
        salePrice: salePrice.value,
        currency: currency.value,
      };

      this.$emit("onEditProduct", editedProduct);
    },
  },
};
</script>

<style scoped>
.modalBackdrop {
  display: flex;
  position: fixed;
  justify-content: flex-end;
  align-items: center;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(47, 44, 44, 0.419);
  transition: opacity 500ms cubic-bezier(0.4, 0, 0.2, 1),
    visibility 500ms cubic-bezier(0.4, 0, 0.2, 1);
  z-index: 999;
}

.modal {
  position: relative;
  padding: 10px 0;
  min-width: 30%;
  height: 100%;
  background-color: white;
}

.title {
  padding: 0 10px;
  margin-bottom: 25px;
  border-bottom: 5px solid var(--var-btn-color);
}
.is-hidden {
  visibility: hidden;
  pointer-events: none;
  opacity: 0;
}

.img {
  margin: 0 auto;
  margin-bottom: 20px;
  height: 200px;
  width: 200px;
  border-radius: 50%;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
}
.productForm {
  padding: 0 10px;
  display: flex;
  flex-direction: column;
  font-size: 10px;
}
.formLabel {
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.formInput {
  padding: 3px 0;
  font-size: 11px;

  color: var(--var-txt-color);
  border: none;
  outline: none;
  border-bottom: 0.5px var(--var-btn-border-color) solid;
}

.formInput:focus {
  border-bottom: 1px var(--var-btn-color) solid;
}
.formSelect {
  border: none;
  outline: none;
  border-bottom: 0.5px var(--var-btn-border-color) solid;
}

.formSelect:focus {
  border-bottom: 1px var(--var-btn-color) solid;
}
.modalBtnBox {
  padding: 10px 15px;
  position: absolute;
  width: 100%;
  bottom: 0;
  border-top: 0.5px var(--var-btn-border-color) solid;
}
.submitBtn {
  padding: 5px;
  margin-right: 5px;
  font-size: 11px;
  background-color: var(--var-btn-color);
  color: white;
  border: none;
  outline: none;
  border: 0.5px var(--var-btn-border-color) solid;
  cursor: pointer;
}

.btn {
  padding: 5px;
  margin-right: 5px;
  font-size: 11px;
  background-color: white;
  border: none;
  outline: none;
  border: 0.5px var(--var-btn-border-color) solid;
  cursor: pointer;
}

.submitBtn:hover,
.submitBtn:focus {
  background-color: #4a8523;

  transform: scale(1.02);
}

.btn:hover,
.btn:focus {
  background-color: var(--var-btn-color);
  color: white;
  transform: scale(1.02);
}
</style>
