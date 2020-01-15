<script>
    import { fade } from 'svelte/transition';
    import Link from './Link.svelte';
    import { sectionEdit } from './stores.js';

    // Expects an object with the following keys:
    // id : unique id to use for reactive naming
    // name : string for the section name
    // children : child link objects
    //
    export let data;
    export let editing;
    let name_edit_active = false;

    $: name_edit_active = editing & name_edit_active;

    function onDblClick(e) {
        console.log(`In dblclick handler for ${data.name}`);
        name_edit_active = true;
        $sectionEdit = data.id;
    }

    function onKeyDown(e) {
        if (e.key === 'Enter') {
            name_edit_active = false;
            data.name = this.value;
        }
    }

    function onBlur(e) {
        // don't update data
        console.log("In blur handler");
        name_edit_active = false;
    }

    function getFocus(el) {
        console.log("Get Focus");
        el.focus();
    }


</script>

<style>
    div {
        background-color : white;
        transition : 1.5s;
    }

    .ls-editing {
        border : 1px solid #aaf;
        margin : 1rem 0.5rem;
    }

    .ls-viewing {
        border : 0;
        margin : 0;
        transition : 1.5s;
    }

    .ls-menu {
        list-style-type: none;
        display: flex;
        justify-content: flex-end;
        margin-block-start: 0;
        margin-block-end: 0;
        padding-inline-start: 0;
        transition : 1.5s ease;
    }

    .ls-menu-item {
        font-size : 0.5rem;
    }

    .ls-h2-editing {
        margin-block-start: 0.25rem;
    }


</style>

<div class:ls-editing={editing} class:ls-viewing={!editing}>
    {#if editing}
        <menu transition:fade class="ls-menu"><button class="ls-menu-item">delete</button></menu>
    {/if}
    {#if name_edit_active && ($sectionEdit === data.id) }
        <input type=text value="{data.name}" on:blur={onBlur} on:keydown={onKeyDown}>
    {:else}
        <h2 class:ls-h2-editing={editing} on:dblclick={onDblClick}>{data.name}</h2>
    {/if}
    <ul>
        {#each data.children as link (link.id)}
            <Link data={link}/>
        {/each}
    </ul>
</div>

