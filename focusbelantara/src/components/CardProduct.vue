<template>
  <div class="card col-md-3 m-4 text-center" @click="redirToDetail(product.id)">
    <div class="c-img mb-1">
        <img :src="`${product.image_url}`" alt="foto" style="width: 18rem" class="mx-auto">
    </div>
    <div class="card-body text-center mt-5">
        <div class="c-title">
            <h5 class="card-title">{{ product.name }}</h5>
        </div>
        <div class="c-price">
            <p class="card-text">{{ product.price }}</p>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardProduct',
  props: ['product'],
  methods: {
    redirToDetail: function (id) {
      if (localStorage.token && localStorage.isLogin) {
        this.$router.push(`/catalog/${id}`)
          .then(_ => {
            this.$toasted.show('Enjoy your shopping ^_^', {
              duration: 3000
            })
          })
          .catch(err => {
            this.$vToastify.error('Require login')
          })
      } else {
        this.$toasted.show('Please login first to go shop', {
          duration: 3000
        })
      }
    }
  }
}
</script>

<style>
.card-body h5 {
  font-weight: bold;
}

.c-img {
  height: 20vh;
}

.c-img img {
  width: 13px;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  background-position: center;
  padding-right: 25px;
}

.c-title, .c-price {
  height: 15vh;
}

.product-desc {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0.5rem 0.5rem;
  text-align: center;
}
.product-desc p {
  margin: 0;
  color: black;
  transition: 0.3s;
}

.product-name {
  cursor: pointer;
}
.product-name:hover {
  transform: scale(1.05);
}

.img-products {
  cursor: pointer;
}
</style>
