<script setup>
    import Navbar from '@/components/Navbar.vue'
    import { RouterView } from 'vue-router';
    import ChatbotWidget from '@/components/ChatbotWidget.vue';
</script>

<template>
    <Navbar />
    <RouterView />
    <ChatbotWidget />
</template>
    