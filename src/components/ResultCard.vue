<template>
  <div class="absolute -bottom-1/2 md:-bottom-1/4 w-full flex justify-center items-center z-10 -translate-1/2">
    <div class="w-4/5 flex flex-col md:flex-row gap-6 items-center md:items-start justify-between md:divide-x 
    bg-white rounded-2xl md:rounded-xl p-6 md:p-10 lg:p-10">
      <ResultItem class="md:self-start md:w-1/4">
        <template #title>IP ADDRESS</template>
        <template #content>
          {{dataToShow.ipAddress}}
        </template>
      </ResultItem>

      <ResultItem class="md:self-start md:w-1/4 md:ps-4 mt-2 md:mt-0">
        <template #title>LOCATION</template>
        <template #content>
          {{dataToShow.location}}
        </template>
      </ResultItem>
      
      <ResultItem class="md:self-start md:w-1/4 md:ps-4 mt-2 md:mt-0">
        <template #title>TIMEZONE</template>
        <template #content>
          UTC {{dataToShow.timezone}}
        </template>
      </ResultItem>
      
      <ResultItem class="md:self-start md:w-1/4 md:ps-4 mt-2 md:mt-0">
        <template #title>ISP</template>
        <template #content>
          {{dataToShow.isp}}
        </template>
      </ResultItem>
    </div>
  </div>
</template>

<script>
import ResultItem from "./ResultItem.vue";

export default {
  name: "result-card",
  components: {
    ResultItem,
  },
  props: {
    dataToShow: {
      type: Object,
      required: true
    }
  },
  setup(props, {emit}) {

    return {

    };
  },
};
</script>

<style lang="scss" scoped></style>
