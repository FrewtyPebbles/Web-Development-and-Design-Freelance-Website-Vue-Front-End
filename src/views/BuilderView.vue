<template>
  <SideBar @change-page="page_change" @open-cart="open_cart"></SideBar>
  <div class="builder">
    <SiteSettings v-if="page == 'site_settings'"></SiteSettings>
    <PageSettings v-else-if="page == 'page_settings'" :page_data="load_page_data()" @update-data="(name, data) => update_page(name, data)"></PageSettings>
  </div>
</template>

<script lang="ts">
import router from '@/router';
import { defineComponent } from 'vue';
import SideBar from '@/components/builder/SideBar.vue';
import SiteSettings from '@/components/builder/site/SiteSettings.vue';
import PageSettings, { PageSettingsData } from '@/components/builder/page/PageSettings.vue';

export interface PagesData {
  [key: string] : PageSettingsData
}

export default defineComponent({
  name: 'BuilderView',
  components: {
    SideBar,
    SiteSettings,
    PageSettings
  },
  data() {
    return {
      page: "page_settings",
      cart_open: false,
      page_name:"",
      data:{} as PagesData
    }
  },
  methods: {
    back_to_home() {
      router.push('/')
    },
    page_change(page:string) {
      this.page = page
    },
    open_cart() {
      this.cart_open = !this.cart_open
    },
    update_page(name:string, data: PageSettingsData) {
      if (name === "")
        return
      if (name != this.page_name)
      {
        delete this.data[this.page_name]
        this.page_name = name
      }
      
      this.data[this.page_name] = data;
      console.log(JSON.parse(JSON.stringify(this.data)));
    },
    load_page_data(){
      if (this.data[this.page_name] != undefined)
        return this.data[this.page_name]
      return {
        settings:{
          page_title: "",
          page_notes: "",
          exclude_sitemap: false,
          low_priority: false
        },
        features: []
      }
    }
  }
});
</script>

<style scoped lang="scss">
.builder {
  margin: 0;
  margin-left: calc(6vw + 1px);
  background-color: black;
  max-width:100%;
  min-height: calc(100vh - 2px);
  border-style: solid;
  border-width: 1px;
  border-color: black;
  padding: 0;
}
</style>
