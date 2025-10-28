<template>
	<DefaultLayout bg="gray">
		<SectionTitle title="인풋 가이드" subTitle="인풋에 대한 설명 노출"></SectionTitle>
		<Section>
			<h2 class="h_tit2">형태</h2>
			<Box>
				<Form @submit="onSubmit">
					<Input 
						v-model="form.username" 
						id="user" 
						label="사용자 이름" 
						placeholder="이름을 입력하세요" 
						actionLabel="검색"
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
				
					<InputGroup label="가격 및 옵션" layout="row" gap="xm" actionLabel="검색" :actionHandler="onSearch">
						<Input v-model="form.price" label="금액" unit="원" textAlign="right" />
						<Input v-model="form.discount" label="할인" unit="%" textAlign="right" />
						<Input v-model="form.note" label="메모" placeholder="비고 입력" actionLabel="검색2" :actionHandler="onSearch" />
					</InputGroup>

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
					<Input 
						v-model="form.price" 
						type="text" 
						id="price" 
						unit="원" 
						textAlign="right"
						placeholder="금액을 입력해주세요." 
						:showReset="false" 
						actionLabel="검색" 
						:actionHandler="onSearch" 
					/>

					<InputGroup label="주소" layout="column" gap="0.8rem">
						<Input v-model="form.postcode" placeholder="우편번호" actionLabel="검색" :actionHandler="searchPostcode" />
						<Input v-model="form.address" placeholder="기본주소" />
						<Input v-model="form.detailAddress" placeholder="상세주소" />
					</InputGroup>
				</Form>
			</Box>




			<Box>
				
			</Box>
		</Section>
	</DefaultLayout>
</template>

<script setup>
import Box from '@/components/Box.vue'
import { Form, InputGroup, Input } from '@/components/form'

import { reactive } from 'vue'

const form = reactive({
	postcode: '',
	address: '',
	detailAddress: '',
	phone: '',
	email: ''
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


function searchPostcode() {
  console.log('우편번호 검색 실행')
  // ex) API 호출 가능
}

function onSubmit() {
  console.log('폼 제출', form)
}
</script>

<style scoped>
</style>