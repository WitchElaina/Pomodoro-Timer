<template>
    <div id="timer">{{curTime}}</div>
    <div id="state-info">
        <div id="state" class="info">{{isWorking ? 'Working' : 'Resting'}}</div>
        <div id="turn" class="info"># {{turnCount}}</div>
    </div>
    <div id="buttons">
        <button @click="isPaused = !isPaused">{{isPaused ? 'Start' : 'Pause'}}</button>
        <button @click="resetTimer">Reset</button>
        <button @click="nextState">Next</button>
    </div>
</template>

<script setup>
    import {onMounted,ref,computed} from "vue";

    const timeRemain = ref(1500);
    const isPaused = ref(true);
    const isWorking = ref(true);
    const turnCount = ref(0);

    onMounted(setInterval(() => {
        if (!isPaused.value) {
            timeRemain.value--;
            if (timeRemain.value === 0) {
                nextState();
            }
        }
    }, 1000))

    const curTime = computed(() => {
        const minutes = Math.floor(timeRemain.value / 60);
        const seconds = timeRemain.value % 60;
        return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    });

    const resetTimer = () => {
        timeRemain.value = 1500;
        isWorking.value = true;
        if(isPaused.value) {
            turnCount.value = 0;
        }
        isPaused.value = true;
    }

    const nextState = () => {
        isWorking.value = !isWorking.value;
        if (isWorking.value) {
            turnCount.value++;
            timeRemain.value = 1500;
        } else {
            if (turnCount.value % 4 === 0 && turnCount.value !== 0) {
                timeRemain.value = 900;
            } else {
                timeRemain.value = 300;
            }
        }
    }


</script>

<style scoped>
    * {
        box-sizing: border-box;
        font-family: 'Product Sans', 'Roboto', sans-serif;
    }

    #timer {
        display: flex;
        justify-content: center;
        margin-top: 10rem;
        font-size: 8rem;
        font-weight: bold;
        text-align: center;
    }

    #state-info {
        display: flex;
        justify-content: center;
        margin-top: 1rem;
    }

    .info {
        font-size: 1.5rem;
        margin: 0 0.5rem;
    }

    #buttons {
        display: flex;
        justify-content: center;
        margin-top: 1rem;
    }

    #buttons button {
        margin: 0 0.5rem;
        padding: 0.5rem 1rem;
        font-size: 1.5rem;
        width: 10rem;
        border: none;
        border-radius: 2rem;
    }

    #buttons button:hover {
        cursor: pointer;
        background-color: #dad3d3;
    }

</style>