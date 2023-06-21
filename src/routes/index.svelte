<script>
    import ApplicationWindow from "../lib/ApplicationWindow.svelte";
    import Box from "../lib/Box.svelte";
    import Button from "../lib/Button.svelte";
    import Element from "../lib/Element.svelte";
    let datas = [];
    let ids = [];

    let id_gen = "0123456789abcdef";
    const random_id = () => {
        let id = "";
        for (let i = 0; i < 10; i++) {
            id += id_gen.split("")[Math.floor(Math.random() * 16)];
        }

        return id;
    };

    /* let datas = [
        {
            type: "ApplicationWindow",
            props: {
                id: "ui_appwindow",
                height: 400,
                width: 500,
            },
            children: [
                {
                    type: "Box",
                    props: {
                        id: "ui_box",
                    },
                },
            ],
        },
    ]; */

    let currentItem, currentTarget;
    let elements = {
        ApplicationWindow: {
            type: "ApplicationWindow",
            props: {
                id: "ui_appwindow",
                height: 400,
                width: 500,
                spacing: true,
                orientation: "vertical",
            },
        },
        Box: {
            type: "Box",
            props: { id: "ui_appwindow" },
        },
        Button: {
            type: "Button",
            props: { id: "ui_appwindow" },
        },
    };
    const allowDrop = (e) => {
        e.preventDefault();
    };
    const drag = (e) => {
        // console.log(e);
        currentItem = e.target.id;
        // console.log(currentItem);
    };
    const drop = (e) => {
        currentTarget = e.target.id;
        if (datas.length == 0) {
            datas = [...datas, elements[currentItem]];
        } else {
            let el = find();
            change(datas[0], el.props.id, elements[currentItem]);
        }
    };
    const find = () => {
        return datas.find((data) => data.props?.id == currentTarget);
    };
    const change = (obj, target_id, new_props) => {
        let el = new_props;
        console.log(target_id);
        el.props.id = random_id();
        if (obj.props?.id == target_id) {
            if (obj.children?.length == undefined) {
                console.log("child yok");
                obj.children == [];
                obj.children = [el];
            } else {
                obj.children = [...obj.children, el];
            }
        }

        datas = datas;
    };
</script>

<main class="flex">
    <div class="flex border w-72">
        <ul class="ml-10">
            {#each Object.entries(elements) as [k, v]}
                <li on:dragstart={drag} id={k} draggable="true">
                    {k}
                </li>
            {/each}
        </ul>
    </div>
    <div
        id="contentbox"
        class="w-full p-5 border"
        on:drop={drop}
        on:dragover={allowDrop}
    >
        <Element children={datas} />
    </div>
</main>

<style>
    li {
        @apply bg-blue-100 my-2 px-2 cursor-pointer;
    }
</style>
