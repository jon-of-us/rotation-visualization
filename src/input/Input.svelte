<script>
    import TraceButton from "./TraceButton.svelte";
    import MousePosition from "./mousePosition.svelte";
</script>

<div class="container">
    <MousePosition></MousePosition>
    <TraceButton></TraceButton>
</div>

<style>
    .container {
        position: absolute;
        right: 30px;
        top: 20px;
    }
</style>
