<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel class="product-slider" :nav="false" :dots="false" :autoplay="true">
                        <div class="product-item" v-for="itemProduct in products" :key="itemProduct.id">
                            <div class="pi-pic">
                                <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                <ul>
                                    <li @click="saveKeranjang(itemProduct.id, itemProduct.name, itemProduct.galleries[0].photo, itemProduct.price)" class="w-icon active">
                                        <a href="#">
                                            <i class="icon_bag_alt"></i>
                                        </a>
                                    </li>
                                    <li class="quick-view">
                                        <router-link :to="'/product/'+itemProduct.id">+ Quick View</router-link>
                                    </li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{ itemProduct.type }}</div>
                                <a href="#">
                                    <h5>{{ itemProduct.name }}</h5>
                                </a>
                                <div class="product-price">
                                    ${{ itemProduct.price }}
                                    <span>$35.00</span>
                                </div>
                            </div>
                        </div>
                    </carousel>
                </div>
                <div class="col-lg-12" v-else>
                    Produk kosong
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel'
import axios from 'axios';

export default {
    name: "BannerShayna",
    components: {
        carousel
    },
    data: function(){
        return {
            products: [],   
            keranjangUser: []
        }
    },
    methods: {
        saveKeranjang(idProduct, nameProduct, photoProduct, priceProduct){
          var productStored = {
              "id": idProduct,
              "name": nameProduct,
              "photo": photoProduct,
              "price": priceProduct
          };

          this.keranjangUser.push(productStored);
          const parsed = JSON.stringify(this.keranjangUser);
          localStorage.setItem('keranjangUser', parsed);

          window.location.reload();
      }
    },
    mounted: function(){
        if (localStorage.getItem('keranjangUser')) {
                try {
                    this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
                } catch(e) {
                    localStorage.removeItem('keranjangUser');
                }
            }
        axios
            .get("http://127.0.0.1:8000/api/products")
            .then(res => (this.products = res.data.data.data))
            .catch(err => console.log(err));
    }
}
</script>

<style scoped>
.product-item{
    margin-right: 25px;
}

</style>