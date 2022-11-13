<script lang="ts">
    import twitter from "$lib/images/platforms/twitter.svg";

    export let image: string;
    export let name: string;

    export let twitterHandle: string;

    let twitterURL = "https://twitter.com/" + twitterHandle;
</script>

<div class="relative accent h-full flex flex-col justify-start items-center border-solid border p-3 rounded-2xl">
    <a class="absolute top-5 right-5 w-10" href={twitterURL}>
        <img src={twitter} alt=""/>
    </a>

    <div class="flex justify-center w-40">
        <img class="rounded-max" src={image} alt="Avatar">
    </div>
        
    <hr class="primary w-3/4 my-3" />

    <div class="p-2 h-full flex-col justify-around flex">
        <h2 class="font-bold mb-1">{name}</h2>
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