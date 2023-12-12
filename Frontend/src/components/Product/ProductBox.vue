<template>
  <div class="card h-100 w-100">
    <div class="embed-responsive embed-responsive-16by9">
      <img
        class="card-img-top embed-responsive-item"
        :src="product.imageURL"
        alt="Product Image"
      />
    </div>
    <div class="card-body">
      <router-link :to="{ name: 'ShowDetails', params: { id: product.id } }"
        ><h5 class="card-title">{{ product.name }}</h5></router-link
      >
      <p class="card-text"><sup>$</sup>{{ product.price }}</p>
      <p class="card-text font-italic">
        {{ product.description.substring(0, 65) }}...
      </p>
      <router-link
        id="edit-product"
        :to="{ name: 'EditProduct', params: { id: product.id } }"
        v-show="$route.name == 'AdminProduct'"
      >
        Edit
      </router-link>
      <button
          id="remove-product"
          type="button"
          class="btn mr-3 p-1 py-0"
          @click="deleteProduct()"
          v-show="$route.name == 'AdminProduct'"
        >
          Delete
        </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductBox",
  props: ["product"],
  methods: {
    showDetails() {
      this.$router.push({
        name: "ShowDetails",
        params: { id: this.product.id },
      });
    },
    deleteProduct(){
      axios
        .delete(`http://localhost:8080/product/delete/${this.product.id}`)
        .then(
          (response) => {
            if (response.status == 200) {
              this.$router.go(0);
            }
            this.$emit('fetchData');
          },
          (error) => {
            console.log(error);
          }
        );

    }
  },
};
</script>

<style scoped>
.embed-responsive .card-img-top {
  object-fit: cover;
}

a {
  text-decoration: none;
}

.card-title {
  color: #484848;
  font-size: 1.1rem;
  font-weight: 400;
}

.card-title:hover {
  font-weight: bold;
}

.card-text {
  font-size: 0.9rem;
}

#edit-product {
  float: right;
}
#remove-product{
  background-color: #e37878;
}
</style>
