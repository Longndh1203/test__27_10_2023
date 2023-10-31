<template>
  <div id="test" class="container">
    <form class="form-input">
      <label for="">Name</label>
      <input
        type="text"
        class="form-control"
        placeholder="Name"
        v-model="name_1"
        v-bind:class="{
          'form-control': true,
          'is-invalid': !this.name_1,
        }"
      />

      <label for="">In Stock</label>
      <input
        type="text"
        class="form-control"
        placeholder="Instock"
        v-model="inStock_1"
        v-bind:class="{
          'form-control': true,
          'is-invalid': !this.inStock_1,
        }"
      />
      <label for="">Price</label>
      <input
        type="text"
        class="form-control"
        placeholder="Price"
        v-model="price_1"
        v-bind:class="{
          'form-control': true,
          'is-invalid': !this.price_1,
        }"
      />
      <label for="">Description</label>
      <input
        type="text"
        class="form-control"
        placeholder="Description"
        v-model="description_1"
        v-bind:class="{
          'form-control': true,
          'is-invalid': !this.description_1,
        }"
      />
      <button
        class="btn btn-info rounded-0"
        type="button"
        @click="handleSubmit"
      >
        Submit
      </button>
    </form>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">In Stock</th>
          <th scope="col">Price</th>
          <th scope="col">Description</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in productsFilter" v-bind:key="index">
          <td>{{ item.name }}</td>
          <td>{{ item.inStock }}</td>
          <td>{{ item.price }}</td>
          <td>{{ item.description }}</td>
          <td>
            <b-button
              v-b-modal.modal-prevent-closing
              variant="warning"
              @click="handleEditTask(item)"
              >Edit</b-button
            >
            <b-button
              @click="handleDeleteTask(item)"
              variant="danger"
              class="px-2"
              style="margin-left: 10px"
            >
              Delete
            </b-button>
          </td>
        </tr>
      </tbody>
    </table>

    <ModalEditTask
      :editProduct="editProduct"
      @update-data-from-child="updateData"
    ></ModalEditTask>

    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
    ></b-pagination>
  </div>
</template>

<script>
import ModalEditTask from "./ModalEditTask.vue";
// import _ from "lodash";

export default {
  name: "VueTestTest",

  components: {
    ModalEditTask: ModalEditTask,
  },

  data() {
    return {
      perPage: 2,
      currentPage: 1,

      errName: "",
      errPrice: "",
      errInstock: "",
      errDescription: "",

      editProduct: {},

      products: [
        {
          id: "1",
          name: "SamSung",
          inStock: 323,
          price: 32323,
          description: "SS 23",
        },
        {
          id: "2",
          name: "Iphone",
          inStock: 12,
          price: 123456,
          description: "IP 15",
        },
        {
          id: "3",
          name: "SamSung 6",
          inStock: 323,
          price: 32323,
          description: "SS 23",
        },
        {
          id: "4",
          name: "Iphone 6",
          inStock: 12,
          price: 123456,
          description: "IP 15",
        },
        {
          id: "5",
          name: "SamSung 7",
          inStock: 323,
          price: 32323,
          description: "SS 23",
        },
        {
          id: "6",
          name: "Iphone 7",
          inStock: 12,
          price: 123456,
          description: "IP 15",
        },
        {
          id: "7",
          name: "SamSung 8",
          inStock: 323,
          price: 32323,
          description: "SS 23",
        },
        {
          id: "8",
          name: "Iphone 8",
          inStock: 12,
          price: 123456,
          description: "IP 15",
        },
      ],
    };
  },

  mounted() {},

  methods: {
    cleardata() {
      (this.name_1 = ""),
        (this.inStock_1 = ""),
        (this.price_1 = ""),
        (this.description_1 = "");
    },

    handleSubmit() {
      if (
        !this.name_1 ||
        !this.inStock_1 ||
        !this.price_1 ||
        !this.description_1
      ) {
        return;
      } else {
        this.products.push({
          name: this.name_1,
          inStock: this.inStock_1,
          price: this.price_1,
          description: this.description_1,
          id: Math.floor(Math.random() * 100),
        });
      }
      this.cleardata();
    },
    handleDeleteTask(task) {
      const index = this.products.findIndex((item) => item.name === task.name);
      if (index >= 0) {
        this.products.splice(index, 1);
      }
    },
    handleEditTask(item) {
      this.editProduct = item;
      // console.log(index);
      // this.inStock = this.products[index].inStock;
      // this.price = this.products[index].price;
      // this.description = this.products[index].description;
      // console.log(this.products[index]);
    },

    updateData(val) {
      const productClone = JSON.parse(JSON.stringify(this.products));

      const index = productClone.findIndex((item) => item.id === val.id);

      productClone[index] = val;
      this.products = productClone;
    },
  },
  computed: {
    rows() {
      return this.products.length;
    },
    totalPages() {
      return Math.ceil(this.rows / this.perPage);

      // 50 items / 10 per page = 5 pages
      // 55 items / 10 per page = 6 pages
    },
    productsFilter() {
      return JSON.parse(JSON.stringify(this.products)).slice(
        this.currentPage - 1,
        this.perPage
      );
    },
  },
  updated() {
    // console.log(this.editProduct);
  },
};
</script>

<style>
#test {
  display: flex;
}

.form-input {
  gap: 10px;
  width: 400px;
  display: flex;
  flex-direction: column;
}

.table {
  margin-left: 40px;
}
</style>
