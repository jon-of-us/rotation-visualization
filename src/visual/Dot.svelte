<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";

    export let x: number;
    export let y: number;
    let render: Render;
    $: render = ({ context, width, height }) => {
        context.fillStyle = "white";
        context.beginPath();
        context.arc(x, y, 7, 0, 2 * Math.PI);
        context.fill();
    };
</script>

<Layer {render} />
