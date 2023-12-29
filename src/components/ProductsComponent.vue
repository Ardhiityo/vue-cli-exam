<template>
    <div>
        
        <navbar-component 
        :cart="cart" 
        :cartQty="cartQty" 
        :cartSum="cartSum"    
        @slider-status="sliderStatus" 
        @delete-items="deleteItems">
        </navbar-component>
    
        <h1>IDShop</h1>
    
        <price-slider 
        :max="max" 
        :slider="slider">
        </price-slider>
    
        <products-list 
        :products="products" 
        :max="max"
        @add-items="addItems">
        </products-list>
    
    </div>
</template>

<script>

import PriceSlider from "./PriceSlider.vue";
import ProductsList from "./ProductsList.vue";
import NavbarComponent from "./NavbarComponent.vue";

export default {
    props: ["cart", "cartQty", "cartSum", "max", "slider", "products"],
    components: {
        PriceSlider, ProductsList,
        NavbarComponent
    },
    methods: {
        sliderStatus: function () {
            this.$emit("slider-status");
        },
        deleteItems: function (index) {
            this.$emit("delete-items", index);
        },
        addItems: function (items) {
            this.$emit("add-items", items);
        }
    }

}
</script>