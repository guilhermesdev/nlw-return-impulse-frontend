<template>
	<Popover class="flex flex-col items-end">
		<PopoverPanel>
			<WidgetForm />
		</PopoverPanel>
		<PopoverButton
			class="bg-brand-500 flex justify-center items-center rounded-full p-3 text-white group"
		>
			<PhChatTeardropDots class="w-6 h-6" />

			<span
				class="max-w-0 overflow-hidden group-hover:max-w-xs transition-all duration-500 ease-linear"
			>
				<span class="ml-2"></span>
				Feedback
			</span>
		</PopoverButton>
	</Popover>
</template>

<script setup lang="ts">
	import { PhChatTeardropDots } from 'phosphor-vue';
	import { Popover, PopoverButton, PopoverPanel } from '@headlessui/vue';

	import WidgetForm from '@/components/WidgetForm/index.vue';
</script>
