<script setup>
import { ref } from 'vue';
import Modal from './components/Modal.vue';
import Backdrop from './components/Backdrop.vue';
const modalOpen = ref(false);
function toggleModal() {
    modalOpen.value = !modalOpen.value;
}
const data = {
    packageName: 'Nomad',
    items: [
        { name: 'Radisson', cost: 100, duration: 1, id: 1 }, //duration 1 === 1 day
        { name: 'Mariott', cost: 150, duration: 1, id: 2 },
        { name: 'Evex', cost: 30, duration: 1, id: 3 },
        { name: 'Random', cost: 120, duration: 1, id: 4 },
        { name: 'Biltmore', cost: 400, duration: 1, id: 5 },
        { name: 'test', cost: 4200, duration: 1, id: 64 },
    ],
};
</script>

<template>
    <Modal v-if="modalOpen" :data="data" />
    <Backdrop v-if="modalOpen" @click="toggleModal" />
    <button @click="toggleModal">Click meh</button>
</template>
