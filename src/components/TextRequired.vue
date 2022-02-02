<template>
	<label class="label required" for="name">{{ section }}</label>
	<input
		@input="$emit('update:name', $event.target.value)"
		:value="name"
		class="input"
		type="text"
		:placeholder="section"
		:name="id"
		:id="id"
	/>
</template>

<script setup>
defineProps({
	name: { type: String },
	section: { type: String },
	id: { type: String }
});

defineEmits([
	"update:name"
])
</script>

<style lang="scss">
</style>