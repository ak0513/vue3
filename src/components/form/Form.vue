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

<style scoped>
.form {
	margin-top: var(--spacing_xs)
}

.form .form_label {
	display: flex;
	align-items: center;
	font-size:1.4rem;
	color: var(--black);
}

.form .form_info {
	margin-top:0.8rem;
	font-size: 1.4rem;
}

.form .form_txt {
	margin-top: var(--form-label-margin);
	color:var(--dark);
}

.form .form_tip {
	margin-top: var(--form-label-margin);
	font-size: 1.4rem;
	color:var(--gray);
}

.form .form_item {
	position: relative;
}

.form * + .form_item {
	margin-top: var(--form-item-margin);
}

.form .form_item .row {
	margin-left: calc(var(--gutter8) * -1);
	margin-right: calc(var(--gutter8) * -1);
}

.form .form_item .row > [class^="col"] {
	padding-left: var(--gutter8);
	padding-right: var(--gutter8);
}

.form .form_item .form_label + .form_input,
.form .form_item .form_label + .row {
	margin-top: var(--form-label-margin);
}

.form .form_item [class^="col"] > .form_input:only-child {
	margin-top: 0;
}


.form .form_item_inline {
	display: flex;
	align-items: center;
}

.form .form_item_inline .form_label {
	margin-right: 1.6rem;
}

.form .form_item_inline .form_input,
.form .form_item_inline .form_check,
.form .form_item_inline .form_check {
	margin-top: 0;
}

.form .form_item_inline [class*='wrap'],
.form .form_item_inline .form_group,
.form .form_item_inline .row {
	flex-grow: 1;
}

.form > .form_group + .btn_wrap,
.form > .form_item + .btn_wrap {
	margin-top: 5.0rem;
}

.form > .form_item + .form_tit {
	margin-top: 8.0rem;
}

.form .form_group > * + * {
	margin-top: 0.4rem;
}
</style>
