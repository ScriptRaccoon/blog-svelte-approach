<script lang="ts">
	import { page } from "$app/stores";

	const name = $page.params.name;

	const path_object = import.meta.glob("/src/lib/posts/*.svelte");

	const key = `/src/lib/posts/${name}.svelte`;

	let post_component: ConstructorOfATypedSvelteComponent;

	async function load_component() {
		const import_function = path_object[key];
		if (!import_function) return;
		const module = await import_function();
		if (
			module &&
			typeof module === "object" &&
			"default" in module
		)
			post_component =
				module.default as ConstructorOfATypedSvelteComponent;
	}

	load_component();
</script>

{#if post_component}
	<svelte:component this={post_component} />
{/if}
