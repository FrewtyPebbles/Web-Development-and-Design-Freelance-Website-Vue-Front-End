<template>
	<section class="root">
		<div id="title">
			<h1>Page Settings:</h1>
		</div>
		<div id="Settings-root">
			<div id="page-title-label" class="settings-label">
				<h2 title="This is a title representing this page as part of your entire site.">Page Title:</h2>
			</div>
			<input v-model="page_title" @blur="emit_data()" type="text" id="page-title-input" class="settings-input">
			<textarea v-model="page_notes" @blur="emit_data()" id="page-notes-input" class="settings-input"></textarea>
			<div id="page-notes-label" class="settings-label">
				<h2 title="Include any notes or descriptions about the page here.  This includes a description of the page, services you would like to employ on the page, dynamic content, real-time content, and any other features you have selected.">Page Notes:</h2>
			</div>
			<div id="page-settings-input" class="settings-label">
				<h2 title="These are toggleable settings that change the way this page will be developed.">Toggleable Settings:</h2>
				<div title="Leave this unchecked so long as this page's content is relevant to your website's topic.  Pages with little to no relevant content should not have this checked.  This will not affect pricing." @click="() => {exclude_sitemap = !exclude_sitemap; emit_data();}">
					<input v-model="exclude_sitemap" type="checkbox" name="exclude_from_sitemap" id="seo_checkbox"><span>Exclude from search engines.</span>
				</div>
				<div title="Check this box if this page is not required to be completed by your deadline which you will disclose in the meeting." @click="() => {low_priority = !low_priority; emit_data();}">
					<input v-model="low_priority" type="checkbox" name="low_priority" id="low_priority_checkbox"><span>Mark as low priority.</span>
				</div>
			</div>
			<div id="page-notes-upload" class="settings-label">
				<h3>Upload PDF of Notes (optional):</h3>
				<button id="upload-button">
					<div>
						<svg xmlns="http://www.w3.org/2000/svg" width="28" height="37" viewBox="0 0 28 37" fill="none">
							<path d="M0 0H19L27.5 10V37H0V0Z" fill="#F9EDEE"/>
							<line x1="4" y1="12" x2="19" y2="12" stroke="#EFA9AE" stroke-width="2"/>
							<line x1="4" y1="20" x2="24" y2="20" stroke="#EFA9AE" stroke-width="2"/>
							<line x1="4" y1="27" x2="24" y2="27" stroke="#EFA9AE" stroke-width="2"/>
						</svg>
						<div>
							Upload a File...
						</div>
					</div>
				</button>
			</div>
		</div>
	</section>
</template>

<script setup lang="ts">
const emit = defineEmits<{
	updateData: [data: Settings]
}>()
</script>

<script lang="ts">
import { defineComponent, defineEmits, PropType } from 'vue';

export interface Settings {
		page_title: string,
		page_notes: string,
		exclude_sitemap: boolean,
		low_priority: boolean
}

export default defineComponent({
  name: 'SettingsSection',
  props: {
	settings: {
		type: Object as PropType<Settings>,
		required: true
	}
  },
  data() {
	return {
		page_title:this.settings.page_title,
		page_notes:this.settings.page_notes,
		exclude_sitemap: this.settings.exclude_sitemap,
		low_priority: this.settings.low_priority
	}
  },
  methods: {
	emit_data() {
		let json_package = {
			page_title:this.page_title,
			page_notes:this.page_notes,
			exclude_sitemap: this.exclude_sitemap,
			low_priority: this.low_priority
		}
		this.$emit('updateData', json_package);
	}
  }
});
</script>



<style scoped lang="scss">
.root {
	background-color: #779095;
	grid-row-start: top;
	grid-row-end: middle;
	grid-column-start: start;
	grid-column-end: middle;
	color: white;
	display: flex;
	flex-direction: column;

	#title {
		border-bottom: 1px solid #FFF;
		margin: 0 5%;
	}

	#Settings-root {
		display: grid;
		grid-template-columns: [start] 40% [middle] auto [end];
		grid-template-rows: [top] min-content [middle-start] auto [middle-middle] min-content [middle-end] min-content [bottom];
		column-gap: 5%;
		row-gap: 1rem;
		flex-grow: 1;
		overflow: none;
		margin: 2rem 5%;
		// grid items {
			#page-title-label {
				grid-row-start: top;
				grid-row-end: middle-start;
				grid-column-start: start;
				grid-column-end: middle;
			}
			#page-title-input {
				margin-top: 0;
				grid-row-start: top;
				grid-row-end: middle-start;
				grid-column-start: middle;
				grid-column-end: end;
			}
			#page-notes-label {
				grid-row-start: middle-start;
				grid-row-end: middle-end;
				grid-column-start: start;
				grid-column-end: middle;
			}
			#page-notes-input {
				grid-row-start: middle-start;
				grid-row-end: bottom;
				grid-column-start: middle;
				grid-column-end: end;
				resize:none;
			}
			#page-settings-input {
				grid-row-start: middle-middle;
				grid-row-end: middle-end;
				grid-column-start: start;
				grid-column-end: middle;
				resize:none;
				> div { // Checkbox AND LABEL CONTAINER
					&:hover {
						background: #354043;
						cursor: pointer;
					}
					input:checked {
						filter: drop-shadow(0 0 0.4rem #2cdaf8);
						border: 1px solid #2989a4;
						background-color: #30c5df;
						border: 2px solid #29c3de;
					}
					input {
						:hover {
							cursor: pointer;
						}
						-webkit-appearance:none;
						-o-appearance:none;
						border-radius: 3px;
						border: 2px solid #53757c;
						width: 12px;
						background-color: #618e97;
						filter: drop-shadow(0 0 0.3rem #354043);
					}
					user-select: none;
					display: flex;
					justify-content: space-between;
					margin-top: 0.5rem;
					background: #4F6367;
					padding: 0.3rem;
					border-radius: 10px;
				}
			}
			#page-notes-upload {
				grid-row-start: middle-end;
				grid-row-end: bottom;
				grid-column-start: start;
				grid-column-end: middle;
				display: flex;
				flex-direction: column;
				justify-content: end;
				#upload-button {
					&:hover {
						background: #354043;
						cursor: pointer;
					}
					padding: 0.5rem;
					border-radius: 0.625rem;
					background: #4F6367;
					border: none;
					color: white;
					> div {
						text-align: left;
						display: flex;
						height: fit-content;
						justify-content: space-between;
						width: 100%;
						> div {
							width: calc(100% - 28px);
							height: fit-content;
							transform: translateY(50%);
							text-align: center;
						}
					}
				}
			}
		// } end grid items

		.settings-label {
			> div {
				text-indent: 2rem;
				text-align: left;
				padding: 0;
			}
			h2 {
				margin: 0.25rem;
			}
			h3 {
				padding: 0;
				margin: 0;
				font-size: 1rem;
			}
		}
		
		.settings-input {
			background: linear-gradient(180deg, #F6F8F2 0%, #C5DDE1 100%);
			border-width: 2px;
			border-color: #4F6367;
			border-radius: 10px;
			font-size: 2rem;
			width: auto;
			min-width: 0px;
			+ .settings-input {
				//margin: 0.5rem 1rem 0 1rem;
				font-size: 1rem;
			}
		}
	}
}
</style>