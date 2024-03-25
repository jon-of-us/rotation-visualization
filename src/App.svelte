<script lang="ts">
    import Input from "./input/Input.svelte";
    import { input_store } from "./input/input_store";
    import Canvas from "./canvas/Canvas.svelte";
    import RandomDot from "./visual/RandomDot.svelte";
    import Dot from "./visual/Dot.svelte";
</script>

<div id="app">
    <Input />
    <Canvas>
        <!-- {#each { length: $input_store.slider1 } as _, i}
            <RandomDot />
        {/each}
        <RandomDot /> -->
        <Dot
            x={$input_store.mousePosition.x}
            y={$input_store.mousePosition.y}
        />
    </Canvas>
</div>
