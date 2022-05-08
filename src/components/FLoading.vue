<template>
	<div class="flex justify-center items-center overflow-hidden animate-spin">
		<PhCircleNotch weight="bold" :class="props.iconClass" />
	</div>
</template>

<script setup lang="ts">
	import { PhCircleNotch } from 'phosphor-vue';

	const props = withDefaults(defineProps<{ iconClass?: string }>(), {
		iconClass: 'w-4 h-4'
	});
</script>
