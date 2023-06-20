<script>
    import ApplicationWindow from "../lib/ApplicationWindow.svelte";
    import Box from "../lib/Box.svelte";
    import Button from "../lib/Button.svelte";
    import Element from "../lib/Element.svelte";

    let datas = [
        {
            id: "",
            type: "ApplicationWindow",
            props: {
                height: 400,
                width: 500,
                label: "Test Application",
            },
        },
    ];

    let windows = {
        ApplicationWindow: ApplicationWindow,
    };
    let els = {
        Box: Box,
        Button: Button,
    };
    function dragAndDrop(e) {
        console.log(e);
    }
</script>

<main class="flex">
    <div class="flex border w-72">
        <ul class="ml-10">
            <li
                id="ApplicationWindow"
                on:drop={(e) => dragAndDrop(e)}
                draggable="true"
            >
                ApplicationWindow
            </li>
            <li id="Box" on:drop={dragAndDrop} draggable="true">Box</li>
            <li id="Button" on:drop={dragAndDrop} draggable="true">Button</li>
        </ul>
    </div>
    <div id="contentbox" class="w-full p-5">
        <Element children={datas} />
    </div>
</main>

<style>
    li {
        @apply bg-blue-100 my-2 px-2 cursor-pointer;
    }
</style>
