<script lang="ts">
    export let image: string;
    export let name: string;
</script>

<div class="accent h-full flex flex-col justify-start items-center border-solid border p-3 rounded-2xl">
    <div class="w-full flex flex-col items-center justify-start">
        <div class="flex justify-center items-center bg-white w-28 h-28 border-solid border rounded-max border-white p-1">
            <img class="rounded-max" src={image} alt="Avatar">
        </div>

        <hr class="primary w-3/4 my-3" />
    </div>


    <div class="p-2 h-full flex-col justify-center flex">
        <h2>
            <b>{name}</b>
        </h2>
        <slot></slot>
    </div>

</div>

<style>
    * {
        text-align: center;
    }

    .rounded-max {
        border-radius: 100%;
    }
</style>