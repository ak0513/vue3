<!-- Form.vue -->
<template>
	<div class="form" @submit.prevent="handleSubmit">
		<!-- slot으로 내부 폼 요소를 자유롭게 넣음 -->
		<slot></slot>
	</div>
</template>

<script setup>
import { defineEmits } from 'vue'

// submit 이벤트를 부모로 전달
const emit = defineEmits(['submit'])

function handleSubmit(event) {
	emit('submit', event)
}
</script>

<style>
.form_label {
	display: flex;
	align-items: center;
	font-size: 1.4rem;
	color: var(--gray900);
}

.form_info {
	margin-top:0.8rem;
	font-size: 1.4rem;
}

.form_error {
	color: var(--danger);
	font-size: 1.4rem;
}


.form > .form_item + .form_item,
.form > .form_item + .form_group,
.form > .form_group + .form_group,
.form > .form_group + .form_item {
	margin-top: var(--form-item-margin);
}


/* 폼 레이아웃 */
.form .layout_colume {
	display: flex;
	flex-direction: column;
	gap: var(--gap_md);
}

.form .layout_row {
	display: flex;
	gap: var(--gap_md);
}

.form .layout_row .form_item {
	flex: 1;
}

.form .form_label + .type_checkbox,
.form .form_label + .type_radio {
	margin-top: 1.2rem;
}
</style>
