<script lang="ts">
	import { color } from '../lib/stores.js';
	export let main : string = "Tiny Size\nHuge Performance";
</script>


<div class="p-16" style:background-color={$color}>
	<p class="text-2xl text-black">{main}</p>
</div>
