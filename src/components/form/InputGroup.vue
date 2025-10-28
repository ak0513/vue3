<template>
	<div class="form_group">
		<!-- 그룹 라벨 -->
		<label v-if="label" :for="id" class="form_label">{{ label }}</label>

		<!-- 그룹 input wrapper -->
		<div :class="['input_group', layoutClass]" :style="{ gap }" ref="wrapperRef">
			<!-- slot으로 하위 Input 배치 -->
			<slot></slot>

			<!-- 그룹 액션 버튼 -->
			<Button v-if="actionLabel && actionHandler" :label="actionLabel" size="sm" @click="actionHandler" />
		</div>

		<!-- 그룹 에러 메시지 -->
		<p v-if="error" class="form_info">{{ error }}</p>
	</div>
</template>

<script setup>
import { ref, computed  } from 'vue'
import { Button } from '@/components/form'

const props = defineProps({
	label: { type: String, default: '' },
	id: { type: String, default: '' },
	layout: { type: String, default: 'column', validator: val => ['row', 'column'].includes(val) },
	gap: { type: String, default: '0.8rem' },
	actionLabel: { type: String, default: '' },
	actionHandler: { type: Function, default: null },
	error: { type: String, default: '' },
})

const wrapperRef = ref(null)
const layoutClass = computed(() => `layout-${props.layout}`)

</script>

<style scoped>
</style>
