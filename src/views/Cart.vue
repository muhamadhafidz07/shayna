<template>

    <div>
        <HeaderShayna />
    
        <!-- Breadcrumb Section Begin -->
        <div class="breacrumb-section">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="breadcrumb-text product-more text-left">
                            <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                            <span>Shopping Cart</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Breadcrumb Section Begin -->

        <CartShayna />
    </div>
</template>

<script>

import HeaderShayna from '@/components/HeaderShayna.vue'
import CartShayna from '@/components/CartShayna.vue'

export default {
    name: "Cart",
    components: {
        HeaderShayna,
        CartShayna
    }   

}
</script>