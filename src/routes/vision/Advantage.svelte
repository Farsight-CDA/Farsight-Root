<script lang="ts">
    export let image: string;
    export let title: string;
</script>

<div class="hoverable highlight h-full flex flex-col justify-between items-center border-solid border p-3 rounded-2xl">
    <div class="flex justify-center items-center bg-white w-20 h-20 border-solid border rounded-max border-white p-4">
        <img class="w-full h-full" src={image} alt="">
    </div>

    <hr class="w-3/4 my-3" />

    <h2>
        <b>{title}</b>
    </h2>

    <slot>

    </slot>
</div>

<style>
    * {
        text-align: center;
    }

    .rounded-max {
        border-radius: 100%;
    }

    .hoverable {
        opacity: 100%;
        transition: opacity 0.2s;
    }   

    .hoverable:hover {
        opacity: 70%;
    }
</style>