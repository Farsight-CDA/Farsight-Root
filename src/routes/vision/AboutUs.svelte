<script lang="ts">
    export let image: string;
    export let title: string;
    export let description: string;
</script>

<div class="accent h-full flex flex-col justify-between items-center border-solid border p-3 rounded-2xl">
    <div class="flex justify-center items-center bg-white w-28 h-28 border-solid border rounded-max border-white p-1">
        <img class="rounded-max" src={image} alt="Avatar">
    </div>

    <hr class="primary w-3/4 my-3" />

    <h2>
        <b>{title}</b>
    </h2>

    <p>{description}</p>
</div>

<style>
    * {
        text-align: center;
    }

    .rounded-max {
        border-radius: 100%;
    }
</style>