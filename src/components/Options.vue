<template>
    <div id="top" :class="{inactive:!props.showOptions}">
        <div class="option">
            <label for="workTime">Work Time</label>
            <input type="number" id="workTime" v-model="props.options.workTime" min="1" @input="validate">
        </div>
        <div class="option">
            <label for="shortBreakTime">Short Break Time</label>
            <input type="number" id="shortBreakTime" v-model="props.options.shortBreakTime" min="1" @input="validate">
        </div>
        <div class="option">
            <label for="longBreakTime">Long Break Time</label>
            <input type="number" id="longBreakTime" v-model="props.options.longBreakTime" min="1" @input="validate">
        </div>
        <div class="option">
            <label for="turns">Turns</label>
            <input type="number" id="turns" v-model="props.options.turns" min="1" @input="validate">
        </div>
        <div class="option">
            <label for="enableNotifications">Notifications</label>
            <input type="checkbox" id="enableNotifications" v-model="props.options.enableNotifications">
        </div>
    </div>

</template>

<script setup>
    const props = defineProps(['options', 'showOptions']);

    const validate = () => {
        if (props.options.workTime < 1) {
            props.options.workTime = 1;
        }
        if (props.options.shortBreakTime < 1) {
            props.options.shortBreakTime = 1;
        }
        if (props.options.longBreakTime < 1) {
            props.options.longBreakTime = 1;
        }
        if (props.options.turns < 1) {
            props.options.turns = 1;
        }
    }
</script>

<style scoped>
    .inactive {
        opacity: 0;
    }

    #top {
        font-family: 'Product Sans', 'Roboto', sans-serif;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .option {
        width: 20rem;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        margin: 0.2rem;
    }

    .option input,label {
        font-size: 1rem;
        width: 9rem;
    }

    input {
        text-align: right;
        border: none;
        background-color: #E5E5E5;

    }

    #enableNotifications {
        width: min-content;
    }

    /* Chrome, Safari, Edge, Opera */
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    /* Firefox */
    input[type=number] {
        -moz-appearance: textfield;
    }

</style>