<template>
	<section class="root">
		<div id="title">
			<h1>Current Features:</h1>
		</div>
		<div id="features-root">
			<slot />
		</div>
	</section>
</template>

<script setup lang="ts">
const emit = defineEmits<{
	updateData: [id: number]
}>()
</script>

<script lang="ts">
import { defineComponent, defineEmits } from 'vue';

export default defineComponent({
  name: 'CurrentFeaturesSection',
  components: {
  },
  methods: {
    remove_feature(id:number) {
		this.$emit("updateData", id)
	}
  }
});
</script>

<style scoped lang="scss">
.root {
	background: #779095;
	grid-row-start: middle;
	grid-row-end: bottom;
	grid-column-start: start;
	grid-column-end: middle;
	display: grid;
	grid-template-columns: [start] 100% [end];
	grid-template-rows: [top] min-content [middle] auto [bottom];
	color: white;
	height: calc(50vh + 2.5rem);
}
#title {
	border-top: 1px solid #FFF;
	border-bottom: 1px solid #FFF;
	background: #779095;
	margin: 0 5%;
}
#features-root {
	&::-webkit-scrollbar {
		display: none;
	}
	background: linear-gradient(180deg, #779095 0%, #D9D9D9 100%);
	padding: 2rem 5%;
	overflow-y: auto;
}
</style>