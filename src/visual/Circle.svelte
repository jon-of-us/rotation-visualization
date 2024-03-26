<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";
    import * as s from "../settings/settings";

    let render: Render;
    $: render = ({ context, width, height }) => {
        context.strokeStyle = "white";
        context.beginPath();
        context.arc(width / 2, height / 2, s.radius, 2, Math.PI * 3);
        context.stroke();
    };
</script>

<Layer {render} />
