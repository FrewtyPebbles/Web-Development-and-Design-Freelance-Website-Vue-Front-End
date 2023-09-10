<template>
	<div id="root">
		<SettingsSection @update-data="(data:Settings) => update_settings(data)" :settings="page_data.settings"></SettingsSection>
		<AddFeaturesSection @update-data="(id:number) => add_feature(id)">
			<UnaddedFeature
				:id="1"
				title="Dynamically Updated Content Sections"
				:price="[50.00, 150.00]"
				:img-src="(require('@/assets/builder/dynamic_content_icon.png') as string)"
				img-alt="Dynamic Content Icon"
				learn-more-link="/about"
				@feature-added="data => add_feature(data)"
			>
				Include content on this page that is pulled from or based on data from your business's database in a responsive way.
			</UnaddedFeature>
		</AddFeaturesSection>
		<CurrentFeaturesSection @update-data="(id:number) => remove_feature(id)">
			<AddedFeature v-for="(id, index) in features"
				:key="index"
				:id="id"
				title="Dynamically Updated Content Sections"
				:price="[50.00, 150.00]"
				:img-src="(require('@/assets/builder/dynamic_content_icon.png') as string)"
				img-alt="Dynamic Content Icon"
				learn-more-link="/about"
				@feature-removed="data => remove_feature(data)"
			>
				Include content on this page that is pulled from or based on data from your business's database in a responsive way.
			</AddedFeature>
		</CurrentFeaturesSection>
	</div>
</template>

<script setup lang="ts">
const emit = defineEmits<{
	updateData: [name: string, data: PageSettingsData]
}>()
</script>

<script lang="ts">
import router from '@/router';
import { PropType, defineComponent, defineEmits } from 'vue';
import CurrentFeaturesSection from '@/components/builder/page/sections/CurrentFeaturesSection.vue'
import SettingsSection, { Settings } from './sections/SettingsSection.vue';
import AddFeaturesSection from './sections/AddFeaturesSection.vue'
import UnaddedFeature from '../page/components/UnaddedFeature.vue';
import AddedFeature from '@/components/builder/page/components/AddedFeature.vue'

export interface PageSettingsData {
	settings:{
			page_title: string,
			page_notes: string,
			exclude_sitemap: boolean,
			low_priority: boolean
		},
	features: number[]
}

export default defineComponent({
  name: 'PageSettings',
  props: {
	page_data:{ type: Object as PropType<PageSettingsData>, required: true }
  },
  components: {
	CurrentFeaturesSection,
	SettingsSection,
	AddFeaturesSection,
	UnaddedFeature,
	AddedFeature
  },
  data() {
	return {
		settings:{
			page_title:"",
			page_notes:"",
			exclude_sitemap: false,
			low_priority: false
		},
		features:[] as number[]
	}
  },
  methods: {
    update_settings(update:Settings){
		this.settings = update;
		this.update_data();
	},
	add_feature(id:number) {
		this.features.push(id);
		this.update_data();
	},
	remove_feature(id:number) {
		const index = this.features.indexOf(id);
		if (index > -1) {
			this.features.splice(index, 1);
		}
		this.update_data();
	},
	package() {
		return {
			settings: this.settings,
			features: this.features
		}
	},
	update_data() {
		this.$emit('updateData', this.settings.page_title, this.package())
	}
  }
});
</script>

<style scoped lang="scss">
#root {
	height: 100vh;
	width: calc(100% + 2px);
	margin: -1px;
	display: grid;
	grid-template-columns: [start] 64.25910992% [middle] auto [end];
	grid-template-rows: [top] calc(50% - 2.5rem) [middle] auto [bottom];
}
</style>
