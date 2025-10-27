<template>
	<span v-if="isSvg" v-html="imgContent" :class="iconClass"></span>
	<span v-else :class="iconClass">
		<img :src="imgContent" :alt="props.iconAlt" />
	</span>
</template>

<script setup>
import { ref, computed, watchEffect } from 'vue'

// props
const props = defineProps({
	iconName: { type: String, required: true },
	iconSize: { type: String, default: "24", validator: (val) => ["16", "24", "32"].includes(val) },
	iconColor: { type: String, default: 'gray900' },
	iconPosition: { type: String, default: '', validator: (val) => ['', 'left', 'right'].includes(val) },
	iconAlt: { type: String, default: ''},
})

const imgContent = ref('')
const isSvg = computed(() => props.iconName.toLowerCase().endsWith('.svg'))

// 동적 import
const loadImg = async () => {
	try {
		if (isSvg.value) {
			// SVG는 raw로 가져와서 v-html
			const svg = await import(`../assets/icons/${props.iconName}?raw`)
			imgContent.value = svg.default
		} else {
			// PNG 등은 그냥 경로로
			const img = await import(`../assets/icons/${props.iconName}`)
			imgContent.value = img.default
		}
	} catch (e) {
		console.warn(`Image "${props.iconName}" not found.`)
		imgContent.value = ''
	}
}

loadImg()

const iconClass = computed(() => {
	const classes = ['icon'];

	if (props.iconSize) classes.push(`size${props.iconSize}`)
	if (props.iconColor) classes.push(`${props.iconColor}`)
	if (props.iconPosition) classes.push(`${props.iconPosition}`)

	return classes
})

watchEffect(() => {
	// console.log('iconPosition:', props.iconPosition)
	// console.log('icon:', props.iconName, props.iconPosition)
})
</script>

<style>
.icon {
	display: inline-flex;
	justify-content: center;
	align-items: center;
}

.icon svg {
	width: 100%;
	height: 100%;
}

.icon.left {
	margin-right: 0.8rem;
}

.icon.right {
	margin-left: 0.8rem;
}

.icon.size16 svg,
.icon.size16 img {
	width: 1.6rem;
	height: 1.6rem;
}

.icon.size24 svg,
.icon.size24 img {
	width: 2.4rem;
	height: 2.4rem;
}

.icon.size32 svg,
.icon.size32 img {
	width: 3.2rem;
	height: 3.2rem;
}

.icon.gray900 svg {
	fill: var(--gray900)
}

.icon.primary svg {
	fill: var(--primary)
}
</style>
