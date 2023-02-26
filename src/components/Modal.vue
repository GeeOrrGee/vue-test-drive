<script>
import { toRaw } from 'vue';
import PackageItem from './PackageItem.vue';
export default {
    data() {
        return {
            total: 0,
            quantity: 0,
            items: [],
        };
    },
    props: ['data'],

    components: {
        PackageItem,
    },

    methods: {
        updateTotal(value) {
            this.total += value;
        },
        updateQuantity(value) {
            this.quantity += value;
        },
        clearCart() {
            this.items = [];
            this.updateQuantity(this.quantity * -1);
            this.updateTotal(this.total * -1);
        },
        //method for removing 1 subset of multiple items, ex. "3 days of Mariott" will be 0 after calling this method
        clearItems(itemToClear) {
            this.items = this.items.filter(
                (item) => item.id !== itemToClear.id
            );
            this.updateQuantity(itemToClear.quantity * -1);
            this.updateTotal(itemToClear.cost * itemToClear.quantity * -1);
        },
        removeItem(itemToRemove) {
            if (itemToRemove.quantity === 1) {
                this.items = this.items.filter(
                    (item) => item.id !== itemToRemove.id
                );
            } else {
                this.items.forEach((item) => {
                    if (item.id === itemToRemove.id) {
                        item.quantity--;
                    }
                });
            }
            this.updateQuantity(-1);
            this.updateTotal(itemToRemove.cost * -1);
        },
        addItem(itemToAdd) {
            const existing = this.items.some(
                (item) => item.id === itemToAdd.id
            );
            this.updateQuantity(1);
            this.updateTotal(itemToAdd.cost);
            if (existing) {
                this.items = this.items.map((item) => {
                    if (item.id === itemToAdd.id) {
                        item.quantity++;
                    }
                    return item;
                });
            } else {
                itemToAdd.quantity = 1;
                this.items = [...this.items, itemToAdd];
            }
        },
        // updateCart(newItem, newValue) {
        //     if (this.total <= 0 && newValue < 0) return;
        // },
    },

    mounted() {
        this.data.items.forEach((item) => {
            this.addItem(item);
        });
    },
};
</script>

<template>
    <div class="modal-root">
        <h2>Package "{{ data.packageName }}"</h2>
        <ul class="list">
            <PackageItem
                :key="item?.name"
                v-for="item in items"
                :item="item"
                @addItem="addItem"
                @removeItem="removeItem"
                @clearItems="clearItems"
        /></ul>
        <div class="thin-line" />
        <div class="footer-container">
            <p>Total: {{ this.total }}</p>
            <button class="checkout-button">Checkout</button>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.list {
    overflow-y: scroll;
    max-height: 80%;
    padding: 0;
    max-height: 500px;
    height: 100%;
}
.modal-root {
    box-sizing: border-box;
    z-index: 9999;
    max-width: 800px;
    width: 100%;

    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
    padding: 16px;
    border-radius: 16px;
}

.thin-line {
    height: 1px;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.4);
    margin-block: 16px;
}

.footer-container {
    width: 100%;
    display: flex;
}

.checkout-button {
    margin-left: auto;
    border: 1px solid #03c988;
    background-color: white;
    color: #03c988;
    padding-inline: 42px;
    border-radius: 12px;
    &:hover {
        color: white;
        background-color: rgb(3, 201, 136, 0.8);
        cursor: pointer;
        transition: all 0.3s ease-out;
    }
}
</style>
