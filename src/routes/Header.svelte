<script>
	import logo from '$lib/images/logo.png';
</script>

<header class="flex flex-row w-full h-16 primary border-b p-1 ">
	<div class="flex items-center ml-3">
		<img class="w-max-full max-h-full" src={logo} alt="Farsight Logo"/>
	</div>
	<ul class="flex justify-end items-center w-full mr-3 gap-6">
		<li class="border-r border-l border-black">
			<a href="https://docs.farsight-names.de" class="p-3" target="_blank">
				Docs
			</a>
		</li>
		<li>
			<a href="/" class="accent hover:bg-red-700 text-white text-sm px-4 py-2 border rounded-full">
				Go to app
			</a>
		</li>
	</ul>
</header>

<style>
	
</style>
