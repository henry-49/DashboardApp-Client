<template>
    <header>
        <span class="title">
            Reporting / Orders
        </span>
        <button class="button is-primary is-on-header" @click="openCreateModal">
            <Plus_Icon class="nav_icon" />
            New Order
        </button>
    </header>

    <create-order-modal v-if="isCreateModalVisiable" @close-modal="closeModal">

    </create-order-modal>

    <div>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Order date</th>
                    <th>Customer name</th>
                    <th>Product name</th>
                    <th>Required date</th>
                    <th>Shipped name</th>
                    <th>Shipped address</th>
                    <th>Shipped city</th>
                    <th>Shipped postal code</th>
                    <th>Shipped country</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item , i) in orders" :key="i">
                    <td>{{ item.id }}</td>
                    <td>{{ item.order_date }}</td>
                    <td>{{ item.customer.last_name }}</td>
                    <td>{{ item.product.product_name }}</td>
                    <td>{{ item.required_date }}</td>
                    <td>{{ item.shipped_name }}</td>
                    <td>{{ item.shipped_address }}</td>
                    <td>{{ item.shipped_city }}</td>
                    <td>{{ item.shipped_postal_code }}</td>
                    <td>{{ item.shipped_country }}</td>
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

    import { loadOrders } from '@/api/reporting';
    import { defineComponent, onMounted, ref } from 'vue';

    import Edit_Icon from '@/assets/icons/Edit_Icon.vue';
    import Trash_Icon from '@/assets/icons/Trash_Icon.vue';
    import Plus_Icon from '@/assets/icons/Plus_Icon.vue';

    import CreateOrderModal from '../modals/CreateOrderModal.vue';


    export default defineComponent({

        components: {
            CreateOrderModal,
            Edit_Icon,
            Trash_Icon,
            Plus_Icon
        },

        setup() {

            const orders = ref();

            const isCreateModalVisiable = ref(false);

            const openCreateModal = () => {
                isCreateModalVisiable.value = true;
            }

            const closeModal = () => {
                isCreateModalVisiable.value = false;
            }

            const getOrders = async () => {
                orders.value = await loadOrders();
            }

            console.log(orders)
            
            onMounted(() => {
                getOrders()
            })

            return {
                isCreateModalVisiable,
                orders,

                openCreateModal,
                closeModal
            }
        }
        
    })
</script>
<style lang="">
    
</style>