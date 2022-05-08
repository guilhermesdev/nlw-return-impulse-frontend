<template>
	<div>
		<header class="w-full relative">
			<button
				type="button"
				@click="emit('feedbackRestartRequested')"
				class="absolute top-1 left-0"
			>
				<PhArrowLeft
					weight="bold"
					class="w-4 h-4 text-zinc-400 hover:text-zinc-100"
				/>
			</button>

			<div class="flex justify-center items-center gap-2">
				<img
					:src="feedbackTypeInfo.image.source"
					:alt="feedbackTypeInfo.image.alt"
					class="w-6 h-6"
				/>
				<span class="text-xl leading-6">{{ feedbackTypeInfo.title }}</span>
			</div>

			<CloseButton class="absolute top-1 right-0" />
		</header>

		<form class="my-4 w-full" @submit.prevent="submitFeedback">
			<textarea
				v-model.trim="comment"
				class="w-full min-w-[304px] min-h-[112px] text-sm placeholder-zinc-400 text-zinc-100 border-zinc-600 bg-transparent rounded-md focus:border-brand-500 hover:ring-brand-500 ring-1 outline-none resize-none scrollbar-thin scrollbar-thumb-zinc-700 scrollbar-track-transparent"
				placeholder="Conte com detalhes o que está acontecendo"
			></textarea>

			<footer class="flex gap-2 mt-2">
				<ScreenshotButton
					@screenshot-took="screenshot = $event"
					:screenshot="screenshot"
				/>

				<button
					type="submit"
					:disabled="!comment || isSendingFeedback"
					class="bg-brand-500 hover:bg-brand-300 disabled:hover:bg-brand-500 disabled:opacity-50 transition-colors rounded-md border-transparent p-2 flex-1 flex justify-center items-center text-sm outline-none ring-offset-zinc-900 ring-brand-500 focus:ring-2 focus:ring-offset-2"
				>
					<template v-if="isSendingFeedback">
						<FLoading />
					</template>
					<template v-else>
						Enviar feedback
					</template>
				</button>
			</footer>
		</form>
	</div>
</template>

<script setup lang="ts">
	import { ref } from 'vue';
	import { PhArrowLeft } from 'phosphor-vue';

	import { FeedbackType, feedbackTypes } from '@/components/WidgetForm/types';
	import { api } from '@/lib/api';
	import FLoading from '@/components/FLoading.vue';
	import CloseButton from '@/components/CloseButton.vue';
	import ScreenshotButton from '@/components/WidgetForm/ScreenshotButton.vue';

	const props = defineProps<{
		feedbackType: FeedbackType;
	}>();

	const emit = defineEmits<{
		(e: 'feedbackRestartRequested'): void;
		(e: 'feedbackSentChange', payload: boolean): void;
	}>();

	const comment = ref('');
	const screenshot = ref<string | null>(null);
	const isSendingFeedback = ref(false);

	async function submitFeedback() {
		if (!comment.value || isSendingFeedback.value) return;

		isSendingFeedback.value = true;

		await api.post('/feedbacks', {
			type: props.feedbackType,
			comment: comment.value,
			screenshot: screenshot.value
		});

		isSendingFeedback.value = false;

		emit('feedbackSentChange', true);
	}

	const feedbackTypeInfo = feedbackTypes[props.feedbackType];
</script>
