<template>
  <div class="product">
    <HeaderShayna />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more text-left">
                        <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="image_default" alt="" />
                            </div>
                            <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                                <carousel class="product-thumbs-track ps-slider" :nav="false" :autoplay="true">
                                    <div v-for="ss in productDetails.galleries" :key="ss.id"
                                    class="pt" @click="changeImages(ss.photo)" :class="ss.photo == image_default ? 'active' : '' ">
                                        <img :src="ss.photo" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{ productDetails.type }}</span>
                                    <h3>{{ productDetails.name }}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p v-html="productDetails.description">
                                    </p>
                                    <h4>${{ productDetails.price }}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart" >
                                        <a @click="saveKeranjang(productDetails.id, productDetails.name, productDetails.galleries[0].photo, productDetails.price)" href="#" class="primary-btn pd-cart">
                                        Add To Cart
                                        </a>
                                    </router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedShayna />

    <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderShayna from '@/components/HeaderShayna.vue'
import FooterShayna from '@/components/FooterShayna.vue'
import RelatedShayna from '@/components/RelatedShayna.vue'
import carousel from 'vue-owl-carousel'

import axios from 'axios'

export default {
  name: 'product',
  components: {
    HeaderShayna,
    FooterShayna,
    RelatedShayna,
    carousel
  },
  data: function(){
      return{
          image_default: "",
          productDetails: [],
          keranjangUser: []
      }
  },
  methods: {
      changeImages(urlImage) {
          this.image_default = urlImage;
      },
      setDataPicture(data){
          this.productDetails = data;

          this.image_default = data.galleries[0].photo;
      },
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
            .get("http://127.0.0.1:8000/api/products", {
                params: {
                    id: this.$route.params.id
                }
            })
            .then(res => (this.setDataPicture(res.data.data)))

            .catch(err => console.log(err));
    }
}
</script>

<style scoped>
    .pt {
        margin-right: 18px;
    }
</style>
