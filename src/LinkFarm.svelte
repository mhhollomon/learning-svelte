<script>
    import LinkSection from './LinkSection.svelte';

    export let data;
    let editing = true;
    
    function onClick() {
        editing = !editing;
    }

</script>

<style>
    div {
        transition : .3s;
    }

    .lf-editing {
        background-color : #aaa;
        border: 2px solid #77b;
    }
</style>


<button on:click={onClick}>{#if editing}View{:else}Edit{/if}</button>

<div class:lf-editing={editing}>
{#each data as section (section.id)}
<LinkSection data={section} editing={!!editing}/>
{/each}
</div>
