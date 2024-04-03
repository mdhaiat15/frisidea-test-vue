<script setup>
import { ref } from "vue";
import MapComponent from "./components/MapComponent.vue";
import SearchBox from "./components/SearchBox.vue";
import ResultCard from "./components/ResultCard.vue";

const props = defineProps({});

const outputShow = ref({
  ipAddress: '-',
  location:'-',
  timezone: '-',
  isp: '-',
});

const location = ref([0,0])
const setResult = (res) => {
  const resultPrinted = {
    ipAddress: res.ip,
    location:
      res.location.city + "," + res.location.region + "," + res.location.country + ' ' + res.location.postalCode,
    timezone: res.location.timezone,
    isp: res.isp,
  };
  outputShow.value = resultPrinted;
  location.value = [res.location.lat, res.location.lng]
};

</script>

<template>
  <div class="mx-auto">
    <div class="relative z-10 h-80 bg-cover bg-[url('./assets/images/pattern-bg-mobile.png')] md:bg-[url('./assets/images/pattern-bg-desktop.png')]"> 
      <div class="absolute w-full top-5 md:top-5 z-10">
        <SearchBox @set-result="setResult" />
      </div>
      <ResultCard :data-to-show="outputShow"/>
    </div>
    <MapComponent :location="location"/>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
