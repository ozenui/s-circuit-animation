<script lang="ts">
	import Circuit from '$lib/components/Circuit.svelte';
</script>

<main class="relative flex h-screen w-screen flex-col items-center justify-center">
	<div class="h-[1px] w-full bg-gray-100"></div>

	<section class="border-l border-r border-gray-100 py-20">
		<Circuit />
	</section>

	<div class="h-[1px] w-full bg-gray-100"></div>
</main>
