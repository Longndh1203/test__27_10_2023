<template>
  <b-modal
    id="modal-prevent-closing"
    ref="modal"
    title="Submit Your Name"
    @show="showModal"
    @hidden="hideModal"
    @ok="handleEdit"
    >{{ propsClone }}
    <form style="gap: 10px">
      <label for="">Name</label>
      <input
        type="text"
        class="form-control"
        placeholder="Name"
        v-model="propsClone.name"
      />
      <!-- <input
        type="text"
        class="form-control"
        placeholder="Name"
        :value="editProduct.name"
        @keyup="(e) => handleChangeValue(e, 'name')"
      /> -->
      <!-- @keyup="(e) => handleChangeValue(e)"
      @keyup="handleChangeValue" -->
      <label for="">In Stock</label>
      <input
        type="text"
        class="form-control"
        placeholder="Instock"
        v-model="propsClone.inStock"
      />
      <label for="">Price</label>
      <input
        type="text"
        class="form-control"
        placeholder="Price"
        v-model="propsClone.price"
      />
      <!-- <input
        type="text"
        class="form-control"
        placeholder="Price"
        :value="editProduct.price"
        @keyup="(e) => handleChangeValue(e, 'price')"
      /> -->
      <label for="">Description</label>
      <input
        type="text"
        class="form-control"
        placeholder="Description"
        v-model="propsClone.description"
      />
      <!-- <input
        type="text"
        class="form-control"
        placeholder="Description"
        :value="editProduct.description"
        @keyup="(e) => handleChangeValue(e, 'description')"
      /> -->
    </form>
  </b-modal>
</template>

<script>
// import _ from "lodash";

export default {
  name: "VueTestModaltasks",
  props: {
    editProduct: {
      type: Object,
    },
    updateData: {
      type: Function,
    },
  },

  data() {
    return {
      propsClone: {},
      modalShow: false,
    };
  },
  watch: {
    editProduct(val) {
      this.propsClone = JSON.parse(JSON.stringify(val));
    },
  },

  methods: {
    showModal() {
      this.$refs["modal"].show();
    },
    hideModal() {
      this.$refs["modal"].hide();
    },
    handleEdit() {
      this.$emit("update-data-from-child", this.propsClone);
      this.hideModal();
      // console.log(product);
      // const productEdit = { ...product };
      // console.log("ProductEdit", productEdit);
      // console.log(product);
      // console.log("product", this.editProduct);
      // this.propsClone = this.product;
      // console.log("product", this.product);
    },
  },
};
</script>

<style lang="scss" scoped></style>
