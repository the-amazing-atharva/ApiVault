<template>
  <BodyFlex>
    <header>
      <Navbar />
    </header>
    <Sidebar />
    <ContentBody :title="categorySearched.category">
      <template #heroAreaContent>
        <Hero @update:colorScheme="handleChangeScheme" />
      </template>
      <template #topAreaContent>
        <SearchBar @search:apiSearch="handleSearch" />
      </template>
      <template #cardAreaContent>
        <div class="row">
          <LoadingEffect v-if="isLoading" />
          <div
            class="col-12 col-lg-4 col-md-6 mb-4 mb-md-4"
            v-for="api in apiSearched"
            :key="api"
          >
            <a :href="api.Link" style="text-decoration: none">
              <Card
                :title="api.API"
                :subtitle="api.Category"
                :body="api.Description"
                :cors="api.Cors"
                :https="api.HTTPS"
                :auth="api.Auth"
                :faviconSrc="api.Link"
              />
            </a>
          </div>
        </div>
      </template>
      <template #footerArea>
        <Footer :scheme="scheme.color" />
      </template>
    </ContentBody>
  </BodyFlex>
</template>

<script setup>
import ContentBody from "@/layouts/ContentBody.vue";
import SearchBar from "@/components/SearchBar.vue";
import Sidebar from "@/components/Sidebar.vue";
import { onMounted, reactive, ref } from "vue";
import BodyFlex from "@/layouts/BodyFlex.vue";
import Footer from "@/components/Footer.vue";
import Navbar from "@/components/Navbar.vue";
import Card from "@/components/Card.vue";
import Hero from "@/components/Hero.vue";
import getApiData from "@/components/api/randomApis.js";
import LoadingEffect from "@/components/LoadingEffect.vue";

const scheme = reactive({
  color: "dark",
});

const handleChangeScheme = (val) => {
  scheme.color = val;
};

let apiData = ref(null);
let apiSearched = ref(null);
let categorySearched = reactive({
  category: null,
});
let isLoading = ref(true);

const handleSearch = (val, title) => {
  if (title === undefined) {
    categorySearched.category = "RANDOM";
    apiSearched.value = apiData.value;
  } else if (val.length > 0) {
    categorySearched.category = title.value.toUpperCase();
    apiSearched.value = val;
  } else {
    categorySearched.category = "NO MATCH";
    apiSearched.value = apiData.value;
  }
};

onMounted(async () => {
  apiData.value = await getApiData();
  isLoading.value = false;
});
</script>
