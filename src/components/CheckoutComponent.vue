<template>
    <div>
        <h1 class="mt-5 mb-3">Checkout</h1>
        <table class="table">
            <thead class="thead">
                <tr class="text-center">
                    <th scope="col">Action</th>
                    <th scope="col">Products</th>
                    <th scope="col">Price</th>
                    <th scope="col">Qty</th>
                    <th scope="col">Sub-total</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(items, index) in cart" :key="items.product.id" class="text-center">
                    <td>
                        <button class="btn btn-primary" @click="$emit('add-items', items.product)">+</button>
                        <button class="btn btn-outline-danger ml-1" @click="$emit('delete-items', index)">-</button>
                    </td>
                    <td>{{ items.product.name }}</td>
                    <td>
                        <price-component :value="Number(items.product.price)"></price-component>
                    </td>
                    <td>{{ items.qty }}</td>
                    <td>
                        <span>{{ items.qty * items.product.price | currencyFormat }}</span>
                    </td>
                </tr>
                <tr v-if="cart.length" class="text-center">
                    <td>
                        <router-link class="btn btn-sm btn-outline-primary" to="/">Back to Shop</router-link>
                    </td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td>
                        <h5 class="fw-bold">Total: {{ cartSum | currencyFormat }}</h5>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>

import PriceComponent from "./PriceComponent.vue";

export default {
    props: ["cart", "cartSum"],
    components: {
        PriceComponent
    },
    filters: {
        currencyFormat: function (value) {
            return "Rp." + Number.parseFloat(value).toFixed(2);
        }
    },
}
</script>