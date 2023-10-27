<template>
  <div id="test" class="container">
    <form class="form-input">
      <label for="">Name</label>
      <input
        type="text"
        class="form-control"
        placeholder="Name"
        v-model="name"
      />
      <label for="">In Stock</label>
      <input
        type="text"
        class="form-control"
        placeholder="Instock"
        v-model="inStock"
      />
      <label for="">Price</label>
      <input
        type="text"
        class="form-control"
        placeholder="Price"
        v-model="price"
      />
      <label for="">Description</label>
      <input
        type="text"
        class="form-control"
        placeholder="Description"
        v-model="description"
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
        <tr v-for="(item, index) in tasks" v-bind:key="index">
          <td>{{ item.name }}</td>
          <td>{{ item.inStock }}</td>
          <td>{{ item.price }}</td>
          <td>{{ item.description }}</td>
          <td style="gap: 10px">
            <button @click="handleDeleteTask(item)">Del</button>
            <button @click="handleEdit(index)">Edit</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "VueTestTest",

  data() {
    return {
      errName: "Error name",
      errPrice: "Error name",
      errInstock: "Error name",
      errDescription: "Error name",

      isName: false,
      isPrice: false,
      isInStock: false,
      isDescription: false,

      editTask: null,
      tasks: [
        {
          name: "SamSung",
          inStock: 323,
          price: 32323,
          description: "asdfasdf",
        },
        {
          name: "Iphone",
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
      (this.name = ""),
        (this.inStock = ""),
        (this.price = ""),
        (this.description = "");
    },
    validate() {},

    handleSubmit() {
      if (!this.name || !this.inStock || !this.price || !this.description) {
        return;
      } else {
        this.tasks.push({
          name: this.name,
          inStock: this.inStock,
          price: this.price,
          description: this.description,
        });
      }
      this.cleardata();
    },
    handleDeleteTask(task) {
      const index = this.tasks.findIndex((item) => item.name === task.name);
      if (index >= 0) {
        this.tasks.splice(index, 1);
      }
    },
    handleEdit(index) {
      this.name = this.tasks[index].name;
      this.inStock = this.tasks[index].inStock;
      this.price = this.tasks[index].price;
      this.description = this.tasks[index].description;
    },
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
