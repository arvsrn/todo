<script lang="ts">
    import Search from "./Search.svelte";
    import Task from "./Task.svelte";
    import Menu from "./ContextMenu/Main.svelte";
    import MenuOption from "./ContextMenu/Option.svelte";

    import { Update, CrumpledPaper, ListBullet } from "radix-icons-svelte";
    import { clickOutside } from "svelte-use-click-outside";
    import EditableBadge from "./EditableBadge.svelte";

    interface TaskData {
        title: string;
        note: string;
        completed: boolean;
        tag: TaskTag;
    };

    interface TaskTag {
        color: 'red' | 'orange' | 'yellow' | 'green' | 'blue' | 'purple';
        text: string;
    }

    let newTask: string = "";

    let tasks: Array<TaskData> = [
        {
            title: 'Book a table at Sarovar Portico',
            note: 'Lorem ipsum dolor sit amet... Bing chilling is really cool and John Cena is huge.',
            completed: true,
            tag: {
                color: 'blue',
                text: 'Life',
            }
        }
    ];

    let tags: Array<TaskTag> = [
        {
            color: 'red',
            text: 'Amowogus'
        },
        {
            color: 'blue',
            text: 'Sussy',
        }
    ];

    //@ts-ignore
    //more like ignore typescript's dumb ass
    const randomColor = (): 'blue' | 'red' | 'green' | 'purple' | 'orange' | 'yellow' | 'gray' => ['blue', 'red', 'green', 'purple', 'orange', 'yellow', 'gray'][Math.floor(Math.random() * 7)]

    let mousePosition: number[] = [0, 0];
    let showContextMenu: boolean = false;
</script>

<main>
    <div style="display:flex;flex-direction:column;align-items:flex-start;padding:0px;position:absolute;width:600px;height:fit-content;">
        <div style="display:flex;flex-direction:row;align-items:center;padding:0px;gap:10px;width:600px;height:32px; margin-bottom: 40px;">
            <img src="https://pbs.twimg.com/profile_images/1557306330930589697/BeTkzf59_400x400.jpg" alt="" draggable="false">
            <Search></Search>
            <button class="primary">New list</button>
        </div>
        <div style="display:flex;flex-direction:row;align-items:center;padding:10px;gap:10px;width:100%;height:36px;">
            <p style="font-family:'Inter';font-style:normal;font-weight:400;font-size:13px;line-height:16px;color:#707070;user-select:none;">
                Today
            </p>
        </div>
        {#each tasks as task}
        <div style="width: 100%; height: fit-content;" on:contextmenu|preventDefault={event => {
            showContextMenu = true;
            mousePosition = [event.clientX, event.clientY];
        }}>
            <Task completed={task.completed} text={task.title} note={task.note} badge={task.tag} />
        </div>
        {/each}
        <div style="display:flex;flex-direction:column;gap:0px;width:100%;height:fit-content;min-height:36px;border-bottom:1px solid #2E2E2E;">
            <div contenteditable="true" placeholder="Add a new task..." bind:innerHTML={newTask} on:keyup={event => {
                if (event.key == 'Enter') {
                    tasks.push({
                        title: newTask,
                        note: '',
                        completed: false,
                        tag: {
                            color: 'red',
                            text: 'Amowogus',
                        }
                    });
                    tasks = tasks;
                    newTask = "";
                }
            }}></div>
        </div>
    </div>

    {#if showContextMenu}
    <div style="position:absolute;top:{mousePosition[1]}px;left:{mousePosition[0]}px;" use:clickOutside={() => showContextMenu = false} on:contextmenu|preventDefault={() => {}}>
        <Menu bind:showContextMenu={showContextMenu} bind:contextMenuPosition={mousePosition}>
            <MenuOption text="Make recurring" action={() => {}} icon={Update}></MenuOption>
            <MenuOption text="Delete" action={() => {}} icon={CrumpledPaper} key="Del"></MenuOption>
            <MenuOption text="Edit tags" action={() => {}} icon={ListBullet}>
                <div slot="submenu" style="width: 200px;height:fit-content;border-radius:4px;border:1px solid rgba(255, 255, 255, 0.035);padding:4px;background:#232323;display:flex;flex-direction:row;flex-wrap:wrap;gap:4px;box-shadow: 0px 53px 21px rgba(0, 0, 0, 0.01), 0px 30px 18px rgba(0, 0, 0, 0.05), 0px 13px 13px rgba(0, 0, 0, 0.09), 0px 3px 7px rgba(0, 0, 0, 0.1), 0px 0px 0px rgba(0, 0, 0, 0.1);">
                    {#each tags as tag} 
                    <EditableBadge text="{tag.text}" color="{tag.color}" />
                    {/each}
                    <button class="badge" on:click={() => {
                        tags = [...tags, {
                            color: randomColor(),
                            text: 'Amogus',
                        }]
                    }}>+ New</button>
                </div>
            </MenuOption>
        </Menu>
    </div>
    {/if}
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        padding-top: 150px;
        gap: 40px;
        align-items: center;

        width: 100vw;
        height: 100vh;
    }

    img {
        width: 32px;
        height: 32px;

        border: 1px solid #000000;
        border-radius: 16px;

        user-select: none;
    }

    button.primary {
        display: flex;
        flex-direction: row;
        align-items: center;
        padding: 8px 12px;
        gap: 10px;

        width: fit-content;
        height: 32px;

        color: #EAF6FF;
        background: #0091FF;
        border-radius: 5px;

        border: none;

        font-weight: 600;
        font-size: 13px;
        line-height: 15px;
        cursor: pointer;

        transition: background 0.2s var(--ease);
    }

    button.primary:hover {
        background: #369EFF;
    }

    button.badge {
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
        
        background: #343434;
        color: #A0A0A0;

        border: none;
        outline: none;
    }

    button.badge:hover {
        background: #3E3E3E;
    }

    div[contenteditable="true"] {
        min-height: 36px;
        padding: 10px;
        padding-left: 30px;

        font-family: 'Inter';
        font-style: normal;
        font-weight: 400;
        font-size: 13px;
        line-height: 16px;
        
        color: #EDEDED;
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
</style>