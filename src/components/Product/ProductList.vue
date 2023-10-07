<script setup>
    import {ref,onMounted} from "vue";

    const searchField = ["title"];
    const searchValue = ref();

    const items = ref([]);
    const Header = [
        { text: "Title", value: "title" },
        { text: "Unit Price", value: "price"},
        { text: "Items", value: "stock"},
        { text: "Action", value: "action"}
    ];


    onMounted(() => {
        fetch('https://dummyjson.com/products')
        .then(res => res.json())
        .then((res)=>
            items.value = res.products
        );
        
    })
</script>
<template>
        
    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
        <h2 class="mb-3">Product List</h2>
        <input placeholder="title" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-1/4 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 mb-2" type="text" v-model="searchValue">
        <EasyDataTable buttons-pagination alternating :headers="Header" :items="items" :rows-per-page="10" :search-field="searchField"  :search-value="searchValue" border-cell>
            <template #item-action="items">
                <RouterLink  :to="{ name: 'ProductDetails', params: { id: items.id } }" class=""><svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 14">
                        <g stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
                        <path d="M10 10a3 3 0 1 0 0-6 3 3 0 0 0 0 6Z"/>
                        <path d="M10 13c4.97 0 9-2.686 9-6s-4.03-6-9-6-9 2.686-9 6 4.03 6 9 6Z"/>
                        </g>
                    </svg>
                </RouterLink >
            </template> 
        </EasyDataTable>
    </div>

</template>
<style scoped>

</style>
