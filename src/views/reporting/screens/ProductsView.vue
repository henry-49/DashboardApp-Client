<template>
    <header>
        <span class="title">
            Reporting / Products
        </span>
        <button class="button is-primary is-on-header ">
            New Product
        </button>
    </header>

    <div>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Product Name</th>
                    <th>Category</th>
                    <th>Unit Price</th>
                    <th>Units In Stock</th>
                    <th>Units On Order</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item , i) in products" :key="i">
                    <td>{{ item.id }}</td>
                    <td>{{ item.product_name }}</td>
                    <td>{{ item.category.name }}</td>
                    <td>{{ item.unit_price }}</td>
                    <td>{{ item.units_in_stock }}</td>
                    <td>{{ item.units_on_order }}</td>
                    <td>
                        <span>
                            <Edit_Icon class="table_icon" />
                        </span>
                        <span>
                            <Trash_Icon class="table_icon_left" />
                        </span>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>

</template>
<script lang="ts">

import { loadProducts } from '@/api/reporting';
import { defineComponent, onMounted, ref } from 'vue';

import Edit_Icon from '@/assets/icons/Edit_Icon.vue';
import Trash_Icon from '@/assets/icons/Trash_Icon.vue';


export default defineComponent({

    components: {
        Edit_Icon,
        Trash_Icon
    },

    setup() {

        const products = ref()

        const getProducts = async () => {
            products.value = await loadProducts();
        }

        console.log(products)

        onMounted(() => {
            getProducts()
        })

        return {
            products
        }
    }
    
})
</script>
<style lang="">
    
</style>