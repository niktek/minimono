<script lang="ts">
	import { writable, type Writable } from 'svelte/store';

	import ListBox from '$lib/components/ListBox/ListBox.svelte';
	import ListBoxItem from '$lib/components/ListBox/ListBoxItem.svelte';

	// Props
	/** Exposes parent props to this component. */
	export let parent: any;

	// Stores
	import { modalStore } from '$lib/utilities/Modal/stores';
	const storeFlavor: Writable<string> = writable('chocolate');

	function onFormSubmit(): void {
		$modalStore[0].response($storeFlavor);
		modalStore.close();
	}

	// Base Classes
	const cBase: string = 'space-y-4';
</script>

<!-- @component This example creates a simple form modal. -->

<div class="modal-example-form {cBase}">
	<ListBox selected={storeFlavor} regionList="border border-surface-500 p-4 rounded-container-token">
		<ListBoxItem value="chocolate">Chocolate</ListBoxItem>
		<ListBoxItem value="vanilla">Vanilla</ListBoxItem>
		<ListBoxItem value="strawberry">Strawberry</ListBoxItem>
		<ListBoxItem value="peach">Peach</ListBoxItem>
	</ListBox>
	<!-- prettier-ignore -->
	<footer class="modal-footer {parent.regionFooter}">
        <button class="btn {parent.buttonNeutral}" on:click={parent.onClose}>{parent.buttonTextCancel}</button>
        <button class="btn {parent.buttonPositive}" on:click={onFormSubmit}>Select Flavors</button>
    </footer>
</div>
