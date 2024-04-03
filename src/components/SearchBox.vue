<template>
  <div class="w-full flex justify-center items-center">
    <div class="w-4/5 md:w-5/12">
      <div class="font-medium text-2xl md:text-3xl text-center py-2 text-white">
        IP Address Tracker
      </div>
      <div class="flex md:mt-6">
        <input
          type="text"
          name="ipInput"
          id=""
          class="block w-full rounded-l-2xl md:rounded-l-xl border-0 text-sm md:text-lg text-gray-900 placeholder:text-gray-400 sm:text-sm sm:leading-6 p-2 md:p-3"
          placeholder="Search for any IP address or domain"
          v-model="searchInput"
        />
        <button
          type="button"
          class="flex-shrink-0 p-4 md:p-4 rounded-r-2xl md:rounded-r-xl bg-gray-900 active:bg-gray-700 text-white"
          @click="getIpData"
        >
          <img src="../assets/images/icon-arrow.svg" alt="" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from "vue";
import axios from "axios";

export default {
  name: "search-box",
  emits: ["setResult"],
  components: {},
  setup(props, { emit }) {
    const searchInput = ref(null);
    const getIpData = async () => {
      let params;
      const domainPattern = /^(?:[-A-Za-z0-9]+\.)+[A-Za-z]{2,}$/;
      const ipPattern = /^(?:[0-9]{1,3}\.){3}[0-9]{1,3}$/;
      // https://geo.ipify.org/api/v2/country,city?apiKey=at_8lj0PHlYcFwcltIZDAYGOegzYPlnx&domain=smart-ics.com
      if (searchInput.value === null) {
        params = {
          apiKey: import.meta.env.VITE_API_GEO_KEY,
        };
      } else if (searchInput.value.match(ipPattern)) {
        params = {
          apiKey: import.meta.env.VITE_API_GEO_KEY,
          ipAddress: searchInput.value,
        };
      } else if (searchInput.value.match(domainPattern)) {
        params = {
          apiKey: import.meta.env.VITE_API_GEO_KEY,
          domain: searchInput.value,
        };
      } else {
        return;
      }

      const path1 = "country";
      const path2 = "city";
      const url = `${import.meta.env.VITE_API_GEO}${path1},${path2}`;

      await axios
        .get(url, {
          params: params,
        })
        .then((res) => {
          emit("setResult", res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    };

    onMounted(() => {
      getIpData();
    });

    return {
      searchInput,
      getIpData,
    };
  },
};
</script>

<style lang="scss" scoped></style>
