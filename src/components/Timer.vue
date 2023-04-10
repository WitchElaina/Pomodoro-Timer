<template xmlns="http://www.w3.org/1999/html">
    <div id="timer">{{curTimeStr}}</div>
    <div id="state-info">
        <div id="state" class="info">{{isWorking ? 'Working' : 'Resting'}}</div>
        <div id="turn" class="info"># {{turnCount}}</div>
    </div>
    <div id="buttons">
        <button @click="isPaused = !isPaused">{{isPaused ? 'Start' : 'Pause'}}</button>
        <button @click="resetTimer">Reset</button>
        <button @click="nextState">Next</button>
        <button @click="showOptions = !showOptions">Options</button>
    </div>
    <Options :options="options" :showOptions="showOptions"></Options>
</template>

<script setup>
    import {onMounted, ref, computed, reactive, watch} from "vue";
    import Options from "@/components/Options.vue";

    const showOptions = ref(false);
    const options = reactive({
        workTime: 25,
        shortBreakTime: 5,
        longBreakTime: 15,
        turns: 4
    })

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
        return {min: minutes, sec: seconds};
    });

    const curTimeStr = computed(() => {
        const minutes = Math.floor(timeRemain.value / 60);
        const seconds = timeRemain.value % 60;
        return `${minutes < 10 ? '0' + minutes : minutes}:${seconds < 10 ? '0' + seconds : seconds}`;
    });


    const resetTimer = () => {
        timeRemain.value = options.workTime * 60;
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
            timeRemain.value = options.workTime * 60;
        } else {
            if (turnCount.value % options.turns === 0 && turnCount.value !== 0) {
                timeRemain.value = options.longBreakTime * 60;
            } else {
                timeRemain.value = options.shortBreakTime * 60;
            }
        }
    }

    watch(() => options, () => {
        if(isPaused.value)
            resetTimer();
    }, {deep: true})

    const windowTitle = computed(() => {
        let ret = ''
        if (isPaused.value) {
            ret += 'Paused - '
        }
        else {
            if (curTime.value.min < 1)
                ret += ( curTime.value.sec + 's - ' );
            else
                ret += ( curTime.value.min + 'min - ' );
        }
        ret += isWorking.value ? 'Working' : 'Resting'
        return ret;
    })

    watch(windowTitle, () => {
        document.title = windowTitle.value;
    })


</script>

<style>
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
        background-color: #e6e6e6;
    }

    #buttons button:hover {
        cursor: pointer;
        background-color: #dad3d3;
    }

    * {
        transition: all 0.2s ease-in-out;
    }
</style>