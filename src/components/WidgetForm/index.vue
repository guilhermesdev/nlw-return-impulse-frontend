<template>
	<div
		class="bg-zinc-900 p-4 rounded-2xl mb-4 flex flex-col items-center shadow-lg relative w-[calc(100vw-2rem)] md:w-auto"
	>
		<FeedbackSuccessStep
			v-if="isFeedbackSent"
			@feedback-restart-requested="restartForm"
		/>

		<FeedbackTypeStep
			v-else-if="!selectedFeedbackType"
			@feedback-type-change="selectedFeedbackType = $event"
			class="w-full py-8"
		/>

		<FeedbackContentStep
			v-else
			@feedback-restart-requested="restartForm"
			@feedback-sent-change="isFeedbackSent = $event"
			:feedback-type="selectedFeedbackType"
			class="w-full py-8"
		/>

		<footer class="text-xs text-neutral-400">
			Feito com ♥ pela
			<a
				class="underline underline-offset-2"
				href="https://rocketseat.com.br"
				target="_blank"
			>
				Rocketseat
			</a>
		</footer>
	</div>
</template>

<script setup lang="ts">
	import { ref } from 'vue';

	import FeedbackTypeStep from '@/components/WidgetForm/steps/FeedbackTypeStep.vue';
	import FeedbackContentStep from '@/components/WidgetForm/steps/FeedbackContentStep.vue';
	import FeedbackSuccessStep from '@/components/WidgetForm/steps/FeedbackSuccessStep.vue';
	import { FeedbackType } from '@/components/WidgetForm/types';

	const selectedFeedbackType = ref<FeedbackType | null>(null);
	const isFeedbackSent = ref(false);

	function restartForm() {
		isFeedbackSent.value = false;
		selectedFeedbackType.value = null;
	}
</script>
