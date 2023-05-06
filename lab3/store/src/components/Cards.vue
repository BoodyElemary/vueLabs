<template>
  <div
    class="d-flex py-2 bg-dark text-light justify-content-between align-items-baseline px-3"
  >
    <a
      href="#"
      style="color: yellow; text-decoration: none"
      @click.prevent="gotoCart = false"
      >All Books</a
    >
    <div class="d-flex align-items-baseline">
      <p class="me-2">
        [{{ cart.items.length }}]
        {{ cart.items.length == 1 ? 'Book' : 'Books' }} added
      </p>
      <button class="btn btn-primary" @click="gotoCart = True">Wishlist</button>
    </div>
  </div>

  <!-- Products -->
  <div class="row my-1 text-center" v-if="gotoCart == false">
    <div
      class="card m-auto border m-1"
      style="width: 23rem"
      v-for="product in products"
      :key="product.id"
    >
      <img
        :src="product.imgUrl"
        :title="product.productName"
        style="height: 300px; object-fit: cover"
      />
      <h3>{{ product.productName }}</h3>
      <div class="card-footer">
        <div class="align-items-baseline m-auto">
          <p class="badge bg-secondary py-2 fs-6 mx-2">
            Price:{{ currencyFormatter(product.price) }}
          </p>

          <p class="badge bg-secondary py-2 fs-6 mx-2">
            Author: {{ product.author }}
          </p>
          <p class="badge bg-secondary py-2 fs-6 mx-2">
            Category: {{ product.category }}
          </p>
          <p
            class="badge bg-secondary py-2 fs-6 mx-2"
            :class="[product.numberOfPages > 50 ? 'more' : 'less']"
          >
            #Pages: {{ product.numberOfPages }}
          </p>
          <button class="btn btn-primary" @click="addToCart(product)">
            Add To Wishlist
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- cart -->
  <div class="container my-2" v-if="gotoCart == True">
    <h3 class="w-100 text-center text-danger" v-if="cart.items.length == 0">
      No Books In Wishlist
    </h3>
    <table
      class="table table-striped table-bordered text-center"
      v-if="cart.items.length != 0"
    >
      <thead>
        <tr>
          <th>Total Price</th>
          <th>ID</th>
          <th>Name</th>
          <th>Price</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in cart.items" :key="item.product.id">
          <td>
            <img
              :src="item.product.imgUrl"
              :title="item.product.imgUrl"
              style="height: 100px"
            />
          </td>
          <td>{{ item.product.id }}</td>
          <td>{{ item.product.productName }}</td>
          <td>{{ currencyFormatter(item.product.price) }}</td>
          <td>
            <button class="btn btn-danger" @click="decreaseQuantity(item)">
              Remove
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import products from '@/products';
export default {
  mounted() {
    console.log(this.products);
  },
  data: () => ({
    products: products.Products,
    gotoCart: false,
    cart: { items: [] },
  }),
  methods: {
    addToCart(product) {
      if (!this.checkProduct(product)) {
        this.cart.items.push({ product: product, quantity: 1 });
      }
    },
    getTotal() {
      let total = 0;
      for (i = 0; i < this.cart.items.length; i++) {
        total += this.cart.items[i].product.price * this.cart.items[i].quantity;
      }
      return total;
    },
    checkProduct(product) {
      return this.cart.items.some((item) => item.product.id == product.id);
    },
    increaseQuantity(item) {
      item.quantity++;
    },
    decreaseQuantity(item) {
      item.quantity--;
      if (item.quantity == 0) {
        this.cart.items.splice(
          this.cart.items.findIndex(
            (iitem) => iitem.product.id == item.product.id,
          ),
          1,
        );
      }
    },
    currencyFormatter(value) {
      return Intl.NumberFormat('ar-SA', {
        style: 'currency',
        currency: 'SAR',
        minimumFractionDigits: 0,
      }).format(value);
    },
  },
};
</script>

<style>
.more {
  color: rgb(255, 179, 0);
}
.less {
  color: greenyellow;
}
</style>
