<script lang="ts">
    import { input_store } from "../input/input_store";

    let traceOn = $input_store.traceOn;

    function toggleTrace() {
        $input_store.traceOn = !$input_store.traceOn;
        console.log("traceOn", traceOn);
    }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="container">
    <p>{traceOn ? "Trace is on" : "Trace is off"}</p>
    <label class="switch">
        <input type="checkbox" bind:checked={traceOn} on:change={toggleTrace} />
        <span class="slider round"></span>
    </label>
</div>

<style>
    .container {
        position: fixed;
        bottom: 50px;
        right: 20px;
        width: 150px;
        height: 30px;
    }
    p {
        color: white;
        font-size: 22px;
        margin: 0;
        padding: 0;
    }
    .switch {
        position: relative;
        display: inline-block;
        width: 50px;
        height: 24px;
        margin-top: 10px;
        margin-left: 5px;
    }
    .switch input {
        opacity: 0;
        width: 0;
        height: 0;
    }
    .slider {
        position: absolute;
        cursor: pointer;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: #ccc;
        transition: 0.4s;
    }
    .slider:before {
        position: absolute;
        content: "";
        height: 18px;
        width: 18px;
        left: 4px;
        bottom: 4px;
        background-color: white;
        transition: 0.4s;
    }
    input:checked + .slider {
        background-color: #21f344;
    }
    input:focus + .slider {
        box-shadow: 0 0 1px #21f344;
    }
    input:checked + .slider:before {
        transform: translateX(26px);
    }
    .slider.round {
        border-radius: 24px;
    }
    .slider.round:before {
        border-radius: 50%;
    }
</style>
