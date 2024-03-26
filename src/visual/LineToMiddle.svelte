<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";
    import { input_store } from "../input/input_store";

    export let x: number;
    export let y: number;
    let render: Render;
    $: render = ({ context, width, height }) => {
        context.strokeStyle = "rgba(255, 255, 255, 0.5)";
        context.beginPath();
        context.moveTo(
            $input_store.screenMiddle.x,
            $input_store.screenMiddle.y
        );
        context.lineTo(x, y);
        context.lineWidth = 2;
        context.stroke();
    };
</script>

<Layer {render} />
