<script lang="ts">
	import Header from './Header.svelte';
	import Footer from './Footer.svelte';
	import './styles.css';
	import '../app.css';
</script>

<div class="w-screen h-screen flex flex-col">
	<Header />

	<main class="primary w-full h-full overflow-auto">
		<slot />
	</main>

	<Footer />
</div>

<style>

</style>
