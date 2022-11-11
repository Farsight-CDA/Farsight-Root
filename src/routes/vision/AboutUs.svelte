<script lang="ts">
    export let image: string;
    export let name: string;
</script>

<div class="accent h-full flex flex-col justify-between items-center border-solid border p-3 rounded-2xl">
    <div class="flex justify-center items-center bg-white w-28 h-28 border-solid border rounded-max border-white p-1">
        <img class="rounded-max" src={image} alt="Avatar">
    </div>

    <hr class="primary w-3/4 my-3" />

    <h2>
        <b>{name}</b>
    </h2>

    <slot></slot>
</div>

<style>
    * {
        text-align: center;
    }

    .rounded-max {
        border-radius: 100%;
    }
</style>