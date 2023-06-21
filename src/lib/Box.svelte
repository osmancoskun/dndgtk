<script>
    export let props = {};
</script>

<div
    id={props?.id}
    class:gap-5={props?.spacing}
    class:flex-row={props?.orientation == "horizontal"}
    class:flex-col={props?.orientation == "vertical"}
    class="flex border border-slate-800 bg-blue-100 h-10 m-2"
>
    <slot />
</div>
