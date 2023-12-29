<template>
    <nav class="d-flex justify-content-end align-items-center navbar bg-light border-bottom border-body fixed-top">

        <button type="button" class="btn btn-sm btn-outline-primary mr-3 mt-1" @click="$emit('slider-status')">
            <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
        </button>

        <div class="btn-group" v-if="cart.length > 0">
            <button class="btn btn-primary btn-sm dropdown-toggle" type="button" data-toggle="dropdown" aria-haspopup="true"
                aria-expanded="false" id="dropdownMenuButton">
                <span class="badge badge-pill badge-primary"><b>{{ cartQty }}</b></span>
                <svg xmlns="http://www.w3.org/2000/svg" width="25" height="20" fill="currentColor" class="bi bi-cart-plus"
                    viewBox="0 0 16 16">
                    <path d="M9 5.5a.5.5 0 0 0-1 0V7H6.5a.5.5 0 0 0 0 1H8v1.5a.5.5 0 0 0 1 0V8h1.5a.5.5 0 0 0 0-1H9z" />
                    <path
                        d="M.5 1a.5.5 0 0 0 0 1h1.11l.401 1.607 1.498 7.985A.5.5 0 0 0 4 12h1a2 2 0 1 0 0 4 2 2 0 0 0 0-4h7a2 2 0 1 0 0 4 2 2 0 0 0 0-4h1a.5.5 0 0 0 .491-.408l1.5-8A.5.5 0 0 0 14.5 3H2.89l-.405-1.621A.5.5 0 0 0 2 1zm3.915 10L3.102 4h10.796l-1.313 7h-8.17zM6 14a1 1 0 1 1-2 0 1 1 0 0 1 2 0m7 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0" />
                </svg>
                <price-component :value="Number(cartSum)"></price-component>

            </button>
            <div class="dropdown-menu dropdown-menu-right">
                <div v-for="(items, index) in cart" :key="items.product.id" class="m-2">
                    <div class="dropdown-item-text text-nowrap text-right">
                        <span class="badge badge-pill badge-primary mr-1">
                            {{ items.qty }}
                        </span>
                        {{ items.product.name }}
                        <b>{{ items.product.price * items.qty | currencyFormat }}</b>
                        <button class="btn btn-sm btn-danger ml-2" @click.stop="$emit('delete-items', index)">-</button>
                    </div>
                </div>
                <router-link class="btn btn-sm btn-outline-primary float-lg-right mr-4 mb-2 mt-2" to="/checkout">Checkout</router-link>
            </div>
        </div>

    </nav>
</template>

<script>

import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import PriceComponent from "./PriceComponent.vue";

export default {
    components: {
        FontAwesomeIcon,
        PriceComponent
    },
    props: ["cart", "cartSum", "cartQty"],
    filters: {
        currencyFormat: function (value) {
            return "Rp." + Number.parseFloat(value).toFixed(2);
        }
    },
}
</script>