<script lang="ts">
    import { createEventDispatcher } from "svelte";

    export let alphabet: string[];

    const dispatch = createEventDispatcher();

    function type(char: string): void {
        dispatch("type", {
            text: char
        });
    }
</script>

<div>
    {#each alphabet as i, idx (idx)}
        <button on:click={() => type(i)}>{ i == " " ? "_" : i }</button>
    {/each}
</div>

<style>
    div {
        display: flex;
        flex-direction: row;
        gap: 10px;
        padding: 0 10px 0 10px;
        flex-wrap: wrap;
    }

    button {
        background-color: #202020;
        border: none;
        border-radius: 10px;
        padding: 10px;
        font-size: 30px;
        cursor: pointer;
        transition-duration: 250ms;
        width: calc((100% + 10px) / 19 - 10px);
    }

    @media only screen and (max-width: 1000px) {
        button {
            width: calc((100% + 10px) / 10 - 10px);
        }
    }

    button:hover {
        background-color: #404040;
    }
</style>