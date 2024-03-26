<script lang="ts">
    import { Layer, type Render } from "svelte-canvas";
    import { input_store } from "../input/input_store";
    import { mod } from "../generic_utils/math";
    import * as s from "../settings/settings";
    import Dot from "./Dot.svelte";
    import LineToMiddle from "./LineToMiddle.svelte";

    let render: Render;
    $: radius =
        mod($input_store.mouseRadius + s.radius, s.radius * 2) - s.radius;
    $: x =
        $input_store.screenMiddle.x +
        radius * Math.cos($input_store.mouseAngle);
    $: y =
        $input_store.screenMiddle.y +
        radius * Math.sin($input_store.mouseAngle);
</script>

<Dot {x} {y} />
<LineToMiddle {x} {y} />
