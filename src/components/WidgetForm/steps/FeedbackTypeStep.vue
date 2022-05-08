<template>
	<div>
		<header>
			<span class="text-xl leading-6">Deixe seu feedback</span>

			<CloseButton class="absolute top-6 right-6" />
		</header>

		<div class="flex gap-2 w-full py-8">
			<button
				v-for="(item, key) in feedbackTypes"
				:key="key"
				@click="emitFeedbackType(key)"
				class="bg-zinc-800 rounded-lg py-5 w-24 flex-1 flex flex-col items-center gap-2 border-2 border-transparent hover:border-brand-500 focus:border-brand-500 outline-none"
				type="button"
			>
				<img :src="item.image.source" :alt="item.title" />
				<span>
					{{ item.title }}
				</span>
			</button>
		</div>
	</div>
</template>

<script setup lang="ts">
	import { FeedbackType, feedbackTypes } from '@/components/WidgetForm/types';
	import CloseButton from '@/components/CloseButton.vue';

	const emit = defineEmits<{
		(e: 'feedbackTypeChange', value: FeedbackType): void;
	}>();

	function emitFeedbackType(selectedFeedbackType: FeedbackType) {
		emit('feedbackTypeChange', selectedFeedbackType);
	}
</script>
