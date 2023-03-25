<template>
    <div class="timer_card">
        <div class="timer_card_cross" ref="cross" @click="addTimer">
            <svg width="20" height="4" viewBox="0 0 20 4" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect y="3.5" width="3" height="20" transform="rotate(-90 0 3.5)" fill="#9E9E9E"/>
            </svg>
            <svg width="4" height="20" viewBox="0 0 4 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect x="0.5" width="3" height="20" fill="#9E9E9E"/>
            </svg>
        </div>
    </div>
</template>

<script setup>
import store from "@/store/store";

function addTimer(){
    console.log(store.state.timers)
    store.state.timers ++
}

</script>
