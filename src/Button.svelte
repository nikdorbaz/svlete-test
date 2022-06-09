<script>
    import { createEventDispatcher } from "svelte";

    export let keyboard = {};
    export let blocks = {};

    let newBlock = {
        id: 2,
        text: ""
    }

    const addBlock = () => blocks = [newBlock, ...blocks];
</script>

<div class="event-button">
    <input type="text" value={keyboard.text} />

    <div class="event-button_indicator" on:click={addBlock}></div>
</div>

<style>
    .event-button {
        position: relative;
        margin-bottom: 10px;
    }

    .event-button input {
        width: 100%;
        margin-bottom: 0;
    }

    .event-button:hover .event-button_indicator {
        opacity: 1;
    }

    .event-button_indicator {
        width: 10px;
        height: 10px;
        border-radius: 100%;
        background-color: lightblue;
        position: absolute;
        top: 50%;
        right: -5px;
        transform: translateY(-50%);
        opacity: 0;
        cursor: pointer;
    }

    .event-button_indicator:hover {
        transform: scale(1.5) translateY(-30%);
    }
</style>