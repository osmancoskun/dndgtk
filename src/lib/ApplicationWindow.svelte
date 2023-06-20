<script>
    import maximize from "../assets/window-maximize-symbolic.symbolic.png";
    import minimize from "../assets/window-minimize-symbolic.symbolic.png";
    import close from "../assets/window-close-symbolic.symbolic.png";
    export let props = {};
</script>

<div
    class="appwindow shadow-xl"
    style="--height:{props?.height}px;--width:{props?.width}px"
>
    <div class="appheader h-10 w-auto flex justify-between items-center pl-2">
        <div class="w-auto flex gap-1">
            <img alt="" src={close} />
            <img alt="" src={minimize} />
            <img alt="" src={maximize} />
        </div>
        {#if props?.label}
            <label class="text-sm" for="">{props.label}</label>
        {/if}
        <span />
    </div>

    <slot />
</div>

<style>
    .appwindow {
        width: var(--width);
        height: var(--height);
        max-width: var(--width);
        max-height: var(--height);
    }
    .appheader {
        background: #ebebeb;
        border-bottom: 2px solid #d8d8d8;
    }
    .appwindow .appheader {
        border-radius: 10px 10px 0 0;
    }
    img {
        background-color: #d8d8d8;
        @apply h-4 w-4 rounded-xl;
    }
</style>
