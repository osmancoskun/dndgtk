<script>
    import ApplicationWindow from "./ApplicationWindow.svelte";
    import Box from "./Box.svelte";
    import Button from "./Button.svelte";
    import Element from "./Element.svelte";
    let els = {
        ApplicationWindow: ApplicationWindow,
        Box: Box,
        Button: Button,
    };

    export let children = [];
</script>

<div class="m-5">
    {#if children.length > 0}
        {#each children as child}
            {#if child.children && child.children.length > 0}
                <svelte:component this={els[child["type"]]} props={child.props}>
                    <Element children={child.children} />
                </svelte:component>
            {:else}
                <svelte:component
                    this={els[child["type"]]}
                    props={child.props}
                />
            {/if}
        {/each}
    {/if}
</div>
