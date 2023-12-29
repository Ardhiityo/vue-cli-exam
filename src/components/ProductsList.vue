<template>
    <transition-group tag="div" @beforeEnter="before" @enter="enter" @leave="leave">

        <div class="none" v-for="(items, index) in showItem" :key="items.id" :data-index="index">

            <div class="row">
                <div class="col-1 d-flex flex-row align-items-center justify-content-end">
                    <button class="btn btn-primary" @click="$emit('add-items', items)">+</button>
                </div>
                <div class="col-5 d-flex flex-row align-items-center justify-content-center">
                    <img :src="items.image" alt="items.name" class="img-fluid w-75">
                </div>
                <div class="col-6 d-flex flex-column justify-content-center">
                    <h3>{{ items.name }}</h3>
                    <p>{{ items.description }}</p>
                    <h5>
                        <price-component :value="Number(items.price)"></price-component>
                    </h5>
                </div>
            </div>


        </div>

    </transition-group>
</template>

<script>

import PriceComponent from "./PriceComponent.vue";

export default {
    components: {
        PriceComponent
    },
    props: ["products", "max"],
    computed: {
        showItem: function () {
            let max = this.max;
            return this.products.filter(function (items) {
                return Math.trunc(items.price) <= max;
            })
        }
    },
    methods: {
        before: function (el) {
            el.className = "d-none";
        },
        enter: function (el) {
            var delay = el.dataset.index * 100;
            setTimeout(function () {
                el.className = "d-inline-block animate__animated animate__fadeInRight m-3";
            }, delay)
        },
        leave: function (el) {
            var delay = el.dataset.index * 100;
            setTimeout(function () {
                el.className = "d-inline-block animate__animated animate__fadeOutRight m-3";
            }, delay)
        },
    }

}

</script>