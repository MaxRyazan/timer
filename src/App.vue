<template>
    <div class="container">
        <TheTimer v-for="item in store.state.timers" :key="item" />
        <TheNewTimer />
    </div>
</template>

<script setup>
import store from "@/store/store";
import './assets/css/styles.css'
import TheTimer from './components/TheTimer'
import TheNewTimer from "@/components/TheNewTimer";
</script>
