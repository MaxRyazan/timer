<template>
    <div class="timer_card">
        <div class="timer_card-time" >
            <span>{{ Math.round(now) }}</span>
        </div>
        <div class="timer_card-buttons" ref="border" >
            <svg v-if="startVisible"
                 @click="startTimer"
                 class="timer_card-buttons-start"
                 width="17" height="20" viewBox="0 0 17 20" fill="none"
                 xmlns="http://www.w3.org/2000/svg">
                <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E"/>
            </svg>
            <svg v-else
                 @click="stopTimer"
                 class="timer_card-buttons-start"
                 width="10" height="20" viewBox="0 0 10 20" fill="none"
                 xmlns="http://www.w3.org/2000/svg" >
                <rect x="7" width="3" height="20" fill="white"/>
                <rect width="3" height="20" fill="white"/>
            </svg>
            <svg @click="clearTimer"
                 ref="clear"
                 class="timer_card-buttons-start"
                 width="20" height="20" viewBox="0 0 20 20" fill="none"
                 xmlns="http://www.w3.org/2000/svg" >
                <rect width="20" height="20" />
            </svg>
        </div>
    </div>
</template>

<script setup>
import {onMounted, onUnmounted, ref} from "vue";
import store from "@/store/store";

let now = ref(0);
let clear = ref();
let border = ref();

let interval;
let startVisible = true;

function changeBorderColor(){
    border.value.classList.toggle('white_border')
}

function toggleSquareColor(){
    if(clear.value.style.fill === 'rgb(158, 158, 158)') {
        clear.value.style.fill = 'rgb(255, 255, 255)'
    } else {
        clear.value.style.fill = 'rgb(158, 158, 158)'
    }
}


function startTimer(){
    interval = setInterval(() =>  {now.value += 0.2}, 200)
    startVisible = false
    changeBorderColor()
    toggleSquareColor()
}

function clearTimer(){
    if(now.value !== 0){
        clearInterval(interval)
        startVisible = true
        now.value = 0
        changeBorderColor()
        toggleSquareColor()
    }
}

function stopTimer(){
    clearInterval(interval)
    startVisible = true
    changeBorderColor()
    toggleSquareColor()
}

onMounted(() => {
    clear.value.style.fill = 'rgb(158, 158, 158)'
})
onUnmounted(() =>{
    clearInterval(interval)
})
</script>
