<script>
    export let data;
</script>

<style>
li {
    text-align: auto;
}
</style>

<li><a href="{data.url}">{data.name}</a>
{#if typeof data.children !== 'undefined'}
<ul>
    {#each data.children as link (link.id)}
    <svelte:self data={link}/>
    {/each}
</ul>
{/if}
</li>
