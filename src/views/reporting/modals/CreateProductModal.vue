<template>
    <modal @close="closeModal">
        <div class="modal-content">
                <div class="header">
                    <div class="content">
                        <span class="title">Product properties</span>
                        <Close_Icon class="icon" @click="closeModal()" />
                    </div>
                </div>
            

            <label>
                <strong>
                    <small>
                        Supplier
                        <span class="validation-mark">*</span>
                    </small>
                </strong>
            </label>

            <select v-model="supplierId">
                <option value="" disabled selected>Select product</option>
            </select>


            <label>
                <strong>
                    <small>
                        Category
                        <span class="validation-mark">*</span>
                    </small>
                </strong>
            </label>

            <select v-model="categoryId">
                <option value="" disabled selected>Select category</option>
            </select>

            <label>
                <strong>
                    <small>
                        Product name
                        <span class="validation-mark">*</span>
                    </small>
                </strong>
            </label>

            <input type="text" v-model="productName">


            <label>
                <strong>
                    <small>
                        Unit price
                        <span class="validation-mark">*</span>
                    </small>
                </strong>
            </label>

            <input type="number" v-model="unitPrice">


            <label>
                <strong>
                    <small>
                        Units in stock
                        <span class="validation-mark">*</span>
                    </small>
                </strong>
            </label>

            <input type="number" v-model="unitsInStock">

            <label>
                <strong>
                    <small>
                        Units on oder
                        <span class="validation-mark">*</span>
                    </small>
                </strong>
            </label>

            <input type="number" v-model="unitsOnOrder">




            <div class="footer">
                <div class="content">
                    <button class="cancel" @click="closeModal()">CANCEL</button>
                    <button class="confirm" @click="addNewRecord()">CONFIRM</button>
                </div>
            </div>
       
        </div>     
    </modal>
   

</template>


<script lang="ts">
    import Modal from '@/components/common/Modal.vue';

    import Close_Icon from '@/assets/icons/Close_Icon.vue';
    import { defineComponent, ref } from 'vue';


    export default defineComponent({
        components: {
            Close_Icon,
            Modal
        },

        emits: ['close-modal'],

        // _ is a placeholder for props
        setup(_, context){

            const buttonEnable = ref(false)

            const supplierId = ref();
            const categoryId = ref();
            const productName = ref();
            const unitPrice = ref();
            const unitsInStock = ref();
            const unitsOnOrder = ref();

            const addNewRecord = () => {
                closeModal();
            }

            const closeModal = () => {
                // use context emit
                context.emit('close-modal');
            }

            return {
                buttonEnable,
                categoryId,
                supplierId,
                productName,
                unitPrice,
                unitsInStock,
                unitsOnOrder,

                addNewRecord,
                closeModal
            }
        }
    })

</script>