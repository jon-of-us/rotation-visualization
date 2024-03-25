<script>
    import { onMount, onDestroy } from "svelte";
    import { input_store } from "./input_store";

    function handleMouseMove(event) {
        $input_store.mousePosition.x = event.clientX;
        $input_store.mousePosition.y = event.clientY;
    }

    onMount(() => {
        window.addEventListener("mousemove", handleMouseMove);
    });

    onDestroy(() => {
        window.removeEventListener("mousemove", handleMouseMove);
    });
</script>
