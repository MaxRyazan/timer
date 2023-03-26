<template>
    <div class="timer_card">
        <div class="timer_card-time" >
            <span>{{ hours }}{{ minutes }}{{ seconds }}</span>
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
import {computed, onMounted, onUnmounted, ref, watch} from "vue";

let sec = ref(0);
let clear = ref();
let border = ref();
let interval;
let startVisible = true;
let min = ref(0)
let hour = ref(0)


const seconds = computed(() => {
    if(sec.value === 0) return 0
    return (sec.value > 9.4) ? Math.round(sec.value) : ('0' + Math.round(sec.value))
})
const minutes = computed(() => {
    return min.value > 0 ? min.value+':' : ''
})
const hours = computed(() => {
    return hour.value > 0 ? hour.value+':' : ''
})


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
    interval = setInterval(() =>  {sec.value += 0.2}, 200)
    startVisible = false
    changeBorderColor()
    toggleSquareColor()
}

function clearTimer(){
    if(sec.value !== 0){
        clearInterval(interval)
        startVisible = true
        sec.value = 0
        changeBorderColor()
        toggleSquareColor()
    }
}

function stopTimer(){
    clearInterval(interval)
    startVisible = true
    changeBorderColor()
    toggleSquareColor()
    startVisible = true
}

watch(sec, (value) => {
    if(value > 59.4){
        sec.value = 0;
        min.value += 1
        if(min.value > 59){
            min.value = 0;
            hour.value += 1
        }
    }
})

onMounted(() => {
    clear.value.style.fill = 'rgb(158, 158, 158)'
})
onUnmounted(() =>{
    clearInterval(interval)
})
</script>
