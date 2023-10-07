<script setup>
        import { reactive,onBeforeMount} from 'vue';
        import { useRoute } from 'vue-router';
        import axios from 'axios';
        import ProductList from "../Product/ProductList.vue";

        const productDetails = reactive({});
        const route  = useRoute();
        const id     = route.params.id;

        onBeforeMount ( () => {
             axios.get(`https://dummyjson.com/products/${id}`) 
            .then(function(response) {
                if(response.data){
                    productDetails.id = response.data.id
                    productDetails.title = response.data.title
                    productDetails.description = response.data.description
                    productDetails.thumbnail = response.data.thumbnail
                    productDetails.price = response.data.price
                    
                }
            })
            .catch(function(error) {
                console.error(error);
            });
        });

        console.log(productDetails);
</script>
<template>
        
<div class="w-3/4  bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 mb-2">
    <a href="#">
        <img class="p-8 rounded-t-lg" :src="productDetails.thumbnail" alt="product image"/>
    </a>
    <div class="px-5 pb-5">
        <a href="#">
            <h5 class="text-xl font-semibold tracking-tight text-gray-900 dark:text-white">{{productDetails.title}}</h5>
        </a>
        <div class="flex items-center mt-2.5 mb-5">
           
            <span class="">
                {{productDetails.description}}
            </span>
        </div>
        <div class="flex items-center justify-between">
            <span class="text-3xl font-bold text-gray-900 dark:text-white">${{productDetails.price}}</span>
            <a href="#" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add to cart</a>
        </div>
    </div>
</div>

</template>
<style scoped>

</style>