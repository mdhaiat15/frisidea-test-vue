<template>
  <div class="relative z-0 w-full h-[55vh]">
    <div id="mapContainer" class="h-full"></div>
  </div>
</template>

<script>
import { ref, reactive, onMounted, watch } from "vue";
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
  name: "map-component",
  props: {
    location: {
      type: Array,
      default: () => [],
    },
  },
  setup(props, { emit }) {
    const mainMap = ref(null);
    const marker = ref(null);
    const currCenter = ref(null);
    const initLocation = reactive({
      lat: 0,
      lon: 39,
    });
    const ipLocation = ref(null);
    const markerIcon = L.icon({
      iconUrl: "./icon-location.svg",
      // iconSize: [35, 50],
      iconAnchor: [22, 94],
      popupAnchor: [-3, -76],
    });

    const createMapLayer = () => {
      mainMap.value = L.map("mapContainer", {
        zoomControl: false,
      }).setView(props.location, 5);

      L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
      }).addTo(mainMap.value);
      // setmarker(props.location);
      marker.value = L.marker(props.location, {
        icon: markerIcon,
      }).addTo(mainMap.value);
    };

    const setmarker = (loc) => {
      marker.value.setLatLng(loc);
      mainMap.value.setView(loc, 10);
    };

    watch(
      () => props.location,
      (current) => {
        setmarker(current);
      }
    );

    onMounted(() => {
      createMapLayer();
    });

    return {};
  },
};
</script>

<style lang="scss" scoped></style>
