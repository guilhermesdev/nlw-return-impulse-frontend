<template>
	<PopoverButton
		class="text-zinc-400 hover:text-zinc-100"
		title="Fechar formulário"
	>
		<PhX class="w-4 h-4" weight="bold" />
	</PopoverButton>
</template>

<script setup lang="ts">
	import { PopoverButton } from '@headlessui/vue';
	import { PhX } from 'phosphor-vue';
</script>
