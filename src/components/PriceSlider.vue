<template>
    <transition enter-active-class="animated fadeInDown" leave-active-class="animated slideOutRight">
        <div v-if="slider">
            <div class="justify-content-center align-items-center" :class="sliderState" style="margin-top: 80px;">
                <label for="maximum">Max:</label>
                <input type="number" id="maximum" class="form-control w-25 ml-2 text-center" v-model="maxAmount"
                    @change="$parent.$emit('update:max', maxAmount)">

                <input type="range" id="maximum" class="form-control ml-2 w-25" v-model="maxAmount" max="200"
                    @input="$parent.$emit('update:max',maxAmount)">
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    data: function () {
        return {
            maxAmount: 50
        }
    },
    props: ["slider", "max"],
    computed: {
        sliderState: function () {
            return this.slider ? "d-flex" : "d-none";
        },
    }
}
</script>

<style>
.fade-enter,
.fade-leave-to {
    opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
    transition: all 1s ease-in-out;
    -webkit-transition: all 1s ease-in-out;
    -moz-transition: all 1s ease-in-out;
    -ms-transition: all 1s ease-in-out;
    -o-transition: all 1s ease-in-out;
}
</style>