<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";
    import * as s from "../settings/settings";
    import { input_store } from "../input/input_store";

    export let x: number;
    export let y: number;

    export let trace = [{ x: 0, y: 0 }];
    $: {
        x, y;
        trace.push({ x, y });
        if (trace.length > 200) trace.shift();
        if (!$input_store.traceOn) trace = [];
    }
    let render: Render;
    $: render = ({ context, width, height }) => {
        context.fillStyle = "rgba(255,255,255, 0.5)";
        context.beginPath();
        context.arc(x, y, 7, 0, 2 * Math.PI);
        context.fill();

        if (trace.length <= 4) return;

        context.strokeStyle = "rgba(255, 255, 255, 0.5)";
        context.beginPath();
        context.moveTo(trace[3].x, trace[3].y);
        for (let i = 4; i < trace.length; i++) {
            const dist = Math.sqrt(
                Math.pow(trace[i].x - trace[i - 1].x, 2) +
                    Math.pow(trace[i].y - trace[i - 1].y, 2)
            );
            if (dist > s.radius) {
                context.moveTo(trace[i].x, trace[i].y);
                continue;
            }
            context.lineTo(trace[i].x, trace[i].y);
        }
        context.stroke();
    };
</script>

<Layer {render} />
