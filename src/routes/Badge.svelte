<script lang="ts">
    export let text: string;
    export let color: 'red' | 'blue' | 'green' | 'orange' | 'yellow' | 'purple' | 'gray' = 'blue';
</script>

<main class={color}>{text}</main>

<style>
    main {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        padding: 2px 5px;
        gap: 10px;

        width: fit-content;
        height: fit-content;

        border-radius: 5.5px;
        font-size: 11px;

        user-select: none;
    }

    .red {
        background: #481A1D;
        color: #FF6369;
    }

    .blue {
        background: #102A4C;
        color: #52A9FF;
    }

    .green {
        background: #113123;
        color: #4CC38A;
    }

    .orange {
        background: #441F04;
        color: #FF8B3E;
    }

    .yellow {
        background: #352800;
        color: #F0C000;
    }

    .purple {
        background: #3A1E48;
        color: #BF7AF0;
    }

    .gray {
        background: #343434;
        color: #EDEDED;
    }
</style>