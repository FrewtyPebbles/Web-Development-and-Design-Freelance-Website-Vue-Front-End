<template>
	<section class="root">
		<button id="add-feature" @click="add_feature">
			<svg xmlns="http://www.w3.org/2000/svg" width="37" height="37" viewBox="0 0 37 37" fill="none">
				<rect width="30" height="6" rx="3" transform="matrix(0.00678573 -0.999977 0.999977 -0.00678581 14.8979 33.2417)" fill="#EEF5DB"/>
				<rect width="30" height="6" rx="3" transform="matrix(-0.999977 0.00678577 0.00678577 -0.999977 33.4591 21.1559)" fill="#EEF5DB"/>
			</svg>
		</button>
		<img :src="imgSrc" :alt="imgAlt">
		<div id="title">
			<div>
				<span>${{ (price as number[])[0] }}</span>
				-
				<span>${{ (price as number[])[1] }}</span>
			</div>
			<h2>{{ title }}</h2>
		</div>
		<div id="description">
			<div><slot /></div>
			<div v-if="learnMoreLink" id="learn-more">
				<a :href="(learnMoreLink as string)">
					what are {{ title }}?
				</a>
			</div>
		</div>
	</section>
</template>

<script setup lang="ts">
	const emit = defineEmits<{
		featureAdded: [id: number]
	}>()
</script>

<script lang="ts">
import { PropType, defineComponent, defineEmits } from 'vue';

export default defineComponent({
  name: 'UnaddedFeature',
  props: {
	id: {type:Number, required:true},
	price: {type:[Array, Number] as PropType<number[] | number>, required:true},
	title: {type:String, required:true},
	imgSrc: {type:String, required:true},
	imgAlt: {type:String, required:true},
	learnMoreLink: {type:[String, Boolean], default:false}
  },
  methods: {
    add_feature() {
		this.$emit("featureAdded", this.id)
	}
  }
});
</script>

<style scoped lang="scss">
section.root {
	text-align: left;
	border: none;
	display: flex;
	height: fit-content;
	padding: 0.625rem;
	margin: 0 0 1rem 0;
	flex-direction: column;
	gap: 0.625rem;
	border-radius: 10px;
	background-color: #EEF5DB;
	color: black;
	display: grid;
	grid-template-columns: [start] min-content [middle] auto [end-start] min-content [end-end];
	grid-template-rows: [top] min-content [middle] min-content [bottom];
	// grid sections {
		img {
			width: 3.375rem;
			height: 3.375rem;
			grid-row-start: top;
			grid-row-end: middle;
			grid-column-start: start;
			grid-column-end: middle;
		}
		#title {
			grid-row-start: top;
			grid-row-end: middle;
			grid-column-start: middle;
			grid-column-end: end-start;
			h2 {
				margin: 0;
				text-align: right;
			}
			div {
				text-align: right;
			}
		}
		#description {
			grid-row-start: middle;
			grid-row-end: bottom;
			grid-column-start: start;
			grid-column-end: end-start;
			text-indent: 1rem;
		}
		#learn-more {
			width: 100%;
			text-align: right;
			font-size: 0.75rem;
		}
		button {
			&::before {
				position: absolute;
				content: '';
				top: 0;
				right: 0;
				bottom: 0;
				left: 0;
				background-image: linear-gradient(180deg, #00ffe1 0%, #adcaff 100%);
				z-index: -1;
				transition: opacity 0.1s linear;
				opacity: 0;
				border-radius: 0 10px 10px 0;
				cursor: pointer;
			}
			&:hover::before {
				opacity: 1;
				cursor: pointer;
			}
			position: relative;
			grid-row-start: top;
			grid-row-end: bottom;
			grid-column-start: end-start;
			grid-column-end: end-end;
			margin: -0.625rem -0.625rem -0.625rem 0;
			border-radius: 0 10px 10px 0;
			background: linear-gradient(180deg, #daff7c 0%, #00ffea 100%);
			border-style: none;
			font-size: 4rem;
			color: white;
			z-index: 1;
			cursor: pointer;
			user-select: none;
			padding: 0.5rem;
		}
	// } end grid sections
}
</style>