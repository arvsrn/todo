<script lang="ts">
    import Badge from "./Badge.svelte";
    import { clickOutside } from "svelte-use-click-outside";
    import { slide } from "svelte/transition";

    let toggleMain: boolean = false;

    export let completed: boolean = false;
    export let text: string;
    export let badge: { color: 'red' | 'green' | 'blue' | 'purple' | 'orange' | 'yellow', text: string };
    export let note: string;
</script>

<main on:mousedown={() => toggleMain = true} on:keypress={() => {}} class:toggled={toggleMain} use:clickOutside={() => toggleMain = false}>
    <div class="inner">
        <button on:click={() => completed = !completed} class:enabled={completed}>
            {#if completed}
            <svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M9.1744 2.98196C9.40552 3.13308 9.4704 3.44295 9.31928 3.67407L5.91927 8.87409C5.83914 8.99665 5.70933 9.07785 5.56409 9.09641C5.41885 9.11497 5.27279 9.06889 5.16445 8.97041L2.96445 6.97041C2.76012 6.78466 2.74506 6.46844 2.93081 6.26411C3.11657 6.05978 3.43279 6.04472 3.63712 6.23048L5.40321 7.83601L8.48232 3.12682C8.63344 2.8957 8.94328 2.83085 9.1744 2.98196Z" fill="#161616"/>
            </svg>          
            {/if}
        </button>
        <p>{text}</p>
        <Badge text="{badge.text}" color="{badge.color}"></Badge>
    </div>
    
    {#if toggleMain}
        <div contenteditable="true" placeholder="Add note..." spellcheck="false" bind:innerHTML={note}></div>
    {/if}
</main>

<style>
    button {
        width: 14px;
        height: 14px;
        
        background: #282828;
        border-radius: 3px;

        border: none;
        outline: none;
        cursor: pointer;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        transition: background 0.15s var(--ease);
    }

    main {
        display: flex;
        flex-direction: column;
        padding: 0px;
        gap: 0px;

        width: 100%;
        height: fit-content;
        min-height: 36px;

        border-bottom: 1px solid #2E2E2E;
        transition: height 0.2s var(--ease);
    }

    div.inner {
        display: flex;
        flex-direction: row;
        align-items: center;
        padding: 10px;
        gap: 6px;

        width: 100%;
        height: fit-content;
    }

    div[contenteditable="true"] {
        min-height: 26px;
        padding-bottom: 10px;
        padding-left: 30px;

        font-family: 'Inter';
        font-style: normal;
        font-weight: 400;
        font-size: 13px;
        line-height: 16px;
        
        color: #A0A0A0;
        outline: none;
        border: none;
    }

    [placeholder]:empty::before {
        content: attr(placeholder);
        color: #707070; 
        cursor: text;
    }

    [placeholder]:not(:empty):before {
        content: "";
    }

    p {
        font-family: 'Inter';
        font-style: normal;
        font-weight: 400;
        font-size: 13px;
        line-height: 16px;

        color: #A0A0A0;
        transition: color 0.2s var(--ease);
    }

    .enabled {
        background: #EDEDED;
    }

    .toggled, main:hover {
        background: #1C1C1C;
    }

    .toggled p {
        color: #EDEDED;
    }

    main:hover p {
        color: #EDEDED;
    }
</style>