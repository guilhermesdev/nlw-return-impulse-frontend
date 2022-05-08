<template>
	<button
		v-if="props.screenshot"
		type="button"
		class="w-10 h-10 p-1 rounded-md border-transparent flex justify-end items-end text-zinc-400 hover:text-zinc-100 transition-colors"
		:style="{ backgroundImage: `url(${props.screenshot})` }"
	>
		<PhTrash weight="fill" @click="emit('screenshotTook', null)" />
	</button>
	<button
		v-else
    type="button"
		@click="takeScreenshot"
		class="bg-zinc-800 hover:bg-zinc-700 transition-colors rounded-md border-transparent p-2 outline-none ring-offset-zinc-900 ring-brand-500 focus:ring-2 focus:ring-offset-2 group"
	>
		<FLoading v-if="isTakingScreenshot" class="w-6 h-6" />
		<PhCamera
			v-else
			class="w-6 h-6 text-zinc-100 opacity-50 group-hover:opacity-100 transition-opacity"
		/>
	</button>
</template>

<script setup lang="ts">
	import { ref } from 'vue';
	import { PhCamera, PhTrash } from 'phosphor-vue';
	import html2canvas from 'html2canvas';

	import FLoading from '@/components/FLoading.vue';

	const props = defineProps<{ screenshot: string | null }>();

	const emit = defineEmits<{
		(e: 'screenshotTook', payload: string | null): void;
	}>();

	const isTakingScreenshot = ref(false);

	async function takeScreenshot() {
		isTakingScreenshot.value = true;

		const canvas = await html2canvas(document.documentElement);
		const base64image = canvas.toDataURL('image/png');

		emit('screenshotTook', base64image);

		isTakingScreenshot.value = false;
	}
</script>
