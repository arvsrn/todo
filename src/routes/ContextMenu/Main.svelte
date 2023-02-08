<script lang="ts">
    import { clickOutside } from 'svelte-use-click-outside';
    import { fade } from 'svelte/transition';
    
    export let showContextMenu: boolean;
    export let contextMenuPosition: number[];
</script>

<main transition:fade={{duration: 100}}>
    <slot></slot>
</main>

<style>
    main {
        width: 200px;
        height: fit-content;

        border-radius: 4px;
        border: 1px solid rgba(255, 255, 255, 0.035);

        padding: 6px 4px;

        background: #232323;

        display: flex;
        flex-direction: column;
        gap: 0px;

        box-shadow: 0px 53px 21px rgba(0, 0, 0, 0.01), 0px 30px 18px rgba(0, 0, 0, 0.05), 0px 13px 13px rgba(0, 0, 0, 0.09), 0px 3px 7px rgba(0, 0, 0, 0.1), 0px 0px 0px rgba(0, 0, 0, 0.1);
    }
</style>