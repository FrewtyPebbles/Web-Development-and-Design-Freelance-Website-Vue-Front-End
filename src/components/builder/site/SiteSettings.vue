<template>
	<div id="root">
		Site Settings
	</div>
</template>

<script lang="ts">
import router from '@/router';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'SiteSettings',
  methods: {
    
  }
});
</script>

<style scoped lang="scss">
#root {
	background-color: red;
	min-height: 100vh;
	width: calc(100% + 2px);
	margin: -1px;
}
</style>
