<template>
	<section class="root">
		<div id="title">
			<h1>Add Features:</h1>
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
  name: 'AddFeaturesSection',
  components: {
  },
  methods: {
    add_feature(id:number){
		this.$emit("updateData", id)
	}
  }
});
</script>

<style scoped lang="scss">
.root {
	background-color: #4F6367;
	grid-row-start: top;
	grid-row-end: bottom;
	grid-column-start: middle;
	grid-column-end: end;
	color: white;
	border-left: 2px solid #FFF;
	height: 100vh;
	display: grid;
	grid-template-columns: [start] 100% [end];
	grid-template-rows: [top] min-content [middle] auto [bottom];
}

#title {
	border-bottom: 1px solid #FFF;
	margin: 0 5%;
	padding: 0;
}

#features-root {
	&::-webkit-scrollbar {
		display: none;
	}
	padding: 5%;
	background: linear-gradient(180deg, #4F6367 0%, #EEF5DB 100%);
	overflow-y: auto;

}
</style>