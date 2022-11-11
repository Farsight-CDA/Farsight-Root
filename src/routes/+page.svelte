<script lang="ts">
	import { goto } from "$app/navigation";
	import { onMount } from "svelte";

	onMount(() => {
		goto("https://app.farsight-names.de");
	});
</script>

<svelte:head>
	<title>Home</title>
</svelte:head>

<style>

</style>
