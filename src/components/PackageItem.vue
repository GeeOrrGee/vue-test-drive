<script>
export default {
    props: ['item', 'addItem', 'removeItem', 'clearItems'],
    methods: {
        onAdd(value) {
            this.$emit('addItem', value);
        },
        onRemove(value) {
            this.$emit('removeItem', value);
        },
        clearItems(value) {
            this.$emit('clearItems', value);
        },
    },
};
</script>

<template>
    <li class="single-line">
        <img src="../assets/logo.svg" class="img" />
        <div>
            <p class="text">{{ item.name }} </p>
            <p class="text">Cost: {{ item.cost }}</p>
            <p class="text">Count: {{ item.quantity }}</p>
            <p class="text">Total: {{ item.cost * item.quantity }}</p></div
        >
        <div class="buttons-right">
            <button class="button decrement" @click="onRemove(item)">-</button>
            <button class="button increment" @click="onAdd(item)">+</button>
            <button class="button clear" @click="clearItems(item)"
                >Clear</button
            >
        </div>
    </li>
</template>

<style lang="scss" scoped>
.single-line {
    display: flex;
    align-items: center;
    margin-block: 12px;
    @media screen and (max-width: 850px) {
        flex-direction: column;
    }
}

.img {
    width: 80px;
    height: 80px;
}
.buttons-right {
    margin-left: auto;
    display: flex;
    align-items: center;
    @media screen and (max-width: 850px) {
        width: 100%;
        margin: 0;
    }
}
.text {
    display: inline-block;
    margin-inline: 8px;
}
.button {
    width: 45px;
    height: 35px;
    background-color: white;
    border-radius: 2px;
    margin-inline: 6px;
    &:hover {
        cursor: pointer;
        transition: all 0.3s ease-out;
        color: white;
    }
    @media screen and (max-width: 850px) {
        width: 100%;
        margin-inline: 12px;
    }
}

.decrement {
    border: 1px solid #ff0303;
    &:hover {
        background-color: rgb(255, 3, 3, 0.8);
    }
}

.increment {
    border: 1px solid #03c988;
    &:hover {
        background-color: rgb(3, 201, 136, 0.8);
    }
}

.clear {
    border: 1px solid rgb(0, 0, 0, 0.8);
    &:hover {
        background-color: rgb(0, 0, 0, 0.8);
    }
}
</style>
