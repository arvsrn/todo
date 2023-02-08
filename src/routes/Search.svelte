<script lang='ts'>
    import { slide } from "svelte/transition";
    import Badge from "./Badge.svelte";

    let focused: boolean = false;
</script>

<main>
    <input type="text" placeholder="Search your lists..." on:focusin={() => focused = true} on:focusout={() => focused = false}>
    {#if focused}
        <div class="popover" transition:slide={{ duration: 100 }}>
            <div>Today <Badge text="92" color="gray" /></div>
            <div>Meshgradient <Badge text="3" color="gray" /></div>
            <div>DESIGN® <Badge text="32" color="gray" /></div>
        </div>
    {/if}
</main>

<style>
    main {
        flex: 1;
        height: 32px;

        position: relative;
    }

    input[type="text"] {
        width: 100%;
        flex: 1;
        height: 32px;

        font-size: 13px;

        background: #1C1C1C;
        border: 1px solid #2E2E2E;
        border-radius: 5px;

        color: #EDEDED;
        padding: 0px 12px;
        outline: none;

        transition: border-radius 0.15s var(--ease);
    }

    input[type="text"]:hover, input[type="text"]:active {
        border: 1px solid #343434;
    }

    input[type="text"]::placeholder {
        color: #7E7E7E;
        user-select: none;
    }

    input[type="text"]:focus {
        border-radius: 5px 5px 0px 0px;
    }

    div.popover {
        position: absolute;
        top: 32px;
        
        width: 100%;
        height: 96px;

        background: #1C1C1C;
        border: 1px solid #2E2E2E;
        border-top: none;
        border-radius: 0px 0px 5px 5px;

        box-shadow: 0px 53px 21px rgba(0, 0, 0, 0.01), 0px 30px 18px rgba(0, 0, 0, 0.05), 0px 13px 13px rgba(0, 0, 0, 0.09), 0px 3px 7px rgba(0, 0, 0, 0.1), 0px 0px 0px rgba(0, 0, 0, 0.1);
        overflow: hidden;
    }

    div.popover > div {
        width: 100%;
        height: 32px;

        display: flex;
        flex-direction: row;
        align-items: center;
        padding: 8px 12px;
        gap: 6px;

        font-family: 'Inter';
        font-style: normal;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;

        color: #EDEDED;

        transition: background 0.15s var(--ease), color 0.15s var(--ease);
        cursor: pointer;
    }

    div.popover > div:hover {
        background: #232323;
        color: #52A9FF;
    }
</style>