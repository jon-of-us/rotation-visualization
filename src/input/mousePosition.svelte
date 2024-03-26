<script>
    import { onMount, onDestroy } from "svelte";
    import { input_store } from "./input_store";

    function handleMouseMove(event) {
        $input_store.mousePosition.x = event.clientX;
        $input_store.mousePosition.y = event.clientY;
        $input_store.radius = Math.sqrt(
            Math.pow($input_store.screenMiddle.x - event.clientX, 2) +
                Math.pow($input_store.screenMiddle.y - event.clientY, 2)
        );
        $input_store.angle = Math.atan2(
            event.clientY - $input_store.screenMiddle.y,
            event.clientX - $input_store.screenMiddle.x
        );
    }

    onMount(() => {
        window.addEventListener("mousemove", handleMouseMove);
    });

    onDestroy(() => {
        window.removeEventListener("mousemove", handleMouseMove);
    });
</script>
