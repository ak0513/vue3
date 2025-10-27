<template>
	<DefaultLayout bg="gray">
		<SectionTitle title="인풋 가이드" subTitle="인풋에 대한 설명 노출"></SectionTitle>
		<Section>
			<h2 class="h_tit2">형태</h2>
			<Box>
				<div class="form">
					<Input 
						v-model="form.username" 
						id="user" 
						label="사용자 이름" 
						placeholder="이름을 입력하세요" 
						:actionLabel="'검색'"
						:actionHandler="onSearch"
					/>
					<Input 
						v-model="form.email" 
						id="email" 
						type="email" 
						label="이메일" 
						placeholder="example@email.com"
						:error="form.emailError" 
					/>
					<Input 
						v-model="form.price" 
						type="text" 
						id="price" 
						label="금액" 
						unit="원" 
						textAlign="right"
						placeholder="금액을 입력해주세요." 
						:showReset="false" 
						actionLabel="검색" 
						:actionHandler="onSearch" 
					/>
					<!-- 제출 버튼 -->
					<Button label="제출" @click="validateEmail" />
				</div>

			</Box>
			<Box>
				<InputWrap layout="row" gap="1rem">
					<Input v-model="form.username" label="사용자 이름" placeholder="이름 입력" />
					<Input v-model="form.email" label="이메일" placeholder="example@email.com" />
				</InputWrap>

				<InputWrap layout="row" gap="0.8rem">
					<Input v-model="form.price" label="금액" unit="원" textAlign="right" />
					<Input v-model="form.note" label="메모" placeholder="비고 입력" />
				</InputWrap>
			</Box>
		</Section>
	</DefaultLayout>
</template>

<script setup>
import DefaultLayout from '@/layouts/DefaultLayout.vue'
import Section from '@/layouts/Section.vue'
import SectionTitle from '@/components/SectionTitle.vue'
import Box from '@/components/Box.vue'
import Button from '@/components/Button.vue'
import Input from '@/components/Input.vue'
import InputWrap from '@/components/InputWrap.vue'

import { reactive } from 'vue'

const form = reactive({
	username: '',
	email: '',
	password: '',
	price: '',
	note: ''
})

function onSearch() {
	alert('click')
}


// 이메일 유효성 검사 함수
function isValidEmail(email) {
	// 간단한 정규식 예시
	const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
	return regex.test(email)
}

// 제출 버튼 클릭 시 이메일 검사
function validateEmail() {
	if (!form.email) {
		form.emailError = '이메일을 입력해주세요.'
	} else if (!isValidEmail(form.email)) {
		form.emailError = '이메일 형식이 올바르지 않습니다.'
	} else {
		form.emailError = ''
		alert('이메일이 정상입니다: ' + form.email)
	}
}
</script>

<style scoped>
.form {
	margin-top: var(--spacing_xs)
}

.form .form_label {
	display: flex;
	align-items: center;
	font-size: 1.4rem;
	color: var(--black);
}

.form .form_info {
	margin-top: 0.8rem;
	font-size: 1.4rem;
}

.form .form_txt {
	margin-top: var(--form-label-margin);
	color: var(--dark);
}

.form .form_tip {
	margin-top: var(--form-label-margin);
	font-size: 1.4rem;
	color: var(--gray);
}

.form .form_item {
	position: relative;
}

.form *+.form_item {
	margin-top: var(--form-item-margin);
}

.form .form_item .row {
	margin-left: calc(var(--gutter8) * -1);
	margin-right: calc(var(--gutter8) * -1);
}

.form .form_item .row>[class^="col"] {
	padding-left: var(--gutter8);
	padding-right: var(--gutter8);
}

.form .form_item .form_label+.form_input,
.form .form_item .form_label+.row {
	margin-top: var(--form-label-margin);
}

.form .form_item [class^="col"]>.form_input:only-child {
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

.form>.form_group+.btn_wrap,
.form>.form_item+.btn_wrap {
	margin-top: 5.0rem;
}

.form>.form_item+.form_tit {
	margin-top: 8.0rem;
}

.form .form_group>*+* {
	margin-top: 0.4rem;
}
</style>