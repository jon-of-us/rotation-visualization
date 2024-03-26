<script lang="ts">
    import Input from "./input/Input.svelte";
    import { input_store } from "./input/input_store";
    import Canvas from "./canvas/Canvas.svelte";
    import RandomDot from "./visual/RandomDot.svelte";
    import Dot from "./visual/Dot.svelte";
    import Circle from "./visual/Circle.svelte";
    import LineToMiddle from "./visual/LineToMiddle.svelte";
    import Donut from "./input/Donut.svelte";

    let width: number;
    let height: number;
    $: $input_store.screenMiddle = { x: width / 2, y: height / 2 };
</script>

<div id="app">
    <Input />
    <Canvas bind:width bind:height>
        <!-- {#each { length: $input_store.slider1 } as _, i}
            <RandomDot />
        {/each}
        <RandomDot /> -->
        <Dot
            x={$input_store.mousePosition.x}
            y={$input_store.mousePosition.y}
        />
        <Circle />
        <LineToMiddle
            x={$input_store.mousePosition.x}
            y={$input_store.mousePosition.y}
        />
        <Donut />
    </Canvas>
</div>
