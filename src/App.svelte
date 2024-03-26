<script lang="ts">
    import Input from "./input/Input.svelte";
    import { input_store } from "./input/input_store";
    import Canvas from "./canvas/Canvas.svelte";
    import Circle from "./visual/Circle.svelte";
    import LineToMiddle from "./visual/LineToMiddle.svelte";
    import Donut from "./input/Donut.svelte";
    import DotWithLine from "./visual/DotWithLine.svelte";

    let width: number;
    let height: number;
    $: $input_store.screenMiddle = { x: width / 2, y: height / 2 };
</script>

<div id="app">
    <Input />
    <Canvas bind:width bind:height>
        <Circle />
        <Donut />
        <DotWithLine />
    </Canvas>
</div>
