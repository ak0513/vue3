<template>
	<div :class="['input_wrap', layoutClass]">
		<slot></slot>
	</div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
	/** 
	 * layout 옵션
	 * row: 가로 정렬
	 * column: 세로 정렬 (기본)
	 */
	layout: {
		type: String,
		default: 'column',
		validator: val => ['row', 'column'].includes(val)
	},
	/** gap 조절 (단위 rem) */
	gap: {
		type: String,
		default: '1.2rem'
	}
})

const layoutClass = computed(() => props.layout === 'row' ? 'row_layout' : 'column_layout')
</script>

<style scoped>
.input_wrap {
	display: flex;
	flex-direction: column;
	gap: var(--input-wrap-gap, 1.2rem);
}

/* row layout */
.row_layout {
	flex-direction: row;
	flex-wrap: wrap;
}

/* column layout */
.column_layout {
	flex-direction: column;
}
</style>
