<script>
    import { createEventDispatcher } from "svelte";
    import Button from "./Button.svelte";

    export let block = {};
    export let blocks = [];
    export let index = 0;
    const dispatcher = createEventDispatcher();

    let left = block.position.left;
    let top = block.position.top;
    let moving = false;

    function onMouseDown() {
        moving = true;
    }

    function onMouseMove(e) {
        if (moving) {
            left += e.movementX;
            top += e.movementY;

            block.position.left = left;
            block.position.top = top;
        }
    }

    function onMouseUp() {
        moving = false;
    }


    let newBlock = (left,top) => ({
        id: 2,
        text: "",
        position: {
            left,
            top
        },
        keyboards: []
    });
    let newButton = {
        id: 2,
        text: "Новая кнопка",
    };

    const addBlock = () => (blocks = [newBlock(left + 200, top), ...blocks]);
    const addButton = () => (block.keyboards = [newButton, ...block.keyboards]);
    const removeBlock = (index) => (blocks = [...blocks.slice(0, index), ...blocks.slice(index + 1, blocks.length)]);

    console.log(blocks);
</script>

<div
    class="event"
    on:mousedown={onMouseDown}
    style="left: {left}px; top: {top}px;"
>
{left} {top}
    <input type="text" value={block.text} />

    <div class="event-buttons">
        {#if block.keyboards}
            {#each block.keyboards as keyboard}
                <div class="event-button">
                    <input type="text" value={keyboard.text} />

                    <div class="event-button_indicator" on:click={addBlock} />
                </div>
            {/each}
        {/if}

        <button class="event-buttons_add" on:click={addButton}>
            Добавить кнопку
        </button>
    </div>

    <button class="event-remove" on:click={() => removeBlock(index)}>
        X
    </button>
</div>

<svelte:window on:mouseup={onMouseUp} on:mousemove={onMouseMove} />

<style>
    .event {
        border: 1px solid gray;
        width: 200px;
        padding: 10px;
        background-color: #fff;
        position: absolute;
    }

    .event input {
        width: 100%;
    }

    .event-buttons {
        padding: 10px;
    }

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

    .event-buttons_add {
        background-color: #3046ea;
        padding: 10px;
        text-align: center;
        color: #fff;
        width: 100%;
    }

    .event-remove {
        width: 30px;
        height: 30px;
        border-radius: 100%;
        background-color: red;
        position: absolute;
        top: -15px;
        right: -15px;
    }
</style>
