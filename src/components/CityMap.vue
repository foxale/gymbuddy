<template>
  <div class="map-wrap">
    <a href="https://www.maptiler.com" class="watermark"><img
          src="https://api.maptiler.com/resources/logo.svg" alt="MapTiler logo"/></a>
    <div class="map" ref="mapContainer"></div>
  </div>
</template>

<script>
import { Map, NavigationControl, Marker, Popup } from 'maplibre-gl';
import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue';
import zdrofits from '@/assets/zdrofit.json'

export default {
  name: "CityMap",
  setup () {
    const mapContainer = shallowRef(null);
    const map = shallowRef(null);

    onMounted(() => {
      const apiKey = process.env.VUE_APP_API_KEY;


      const initialState = { lng: 21.0122, lat: 52.2297, zoom: 14 };

      map.value = markRaw(new Map({
        container: mapContainer.value,
        style: `https://api.maptiler.com/maps/streets-v2/style.json?key=${apiKey}`,
        center: [initialState.lng, initialState.lat],
        zoom: initialState.zoom
      }));
      map.value.addControl(new NavigationControl(), 'top-right');
      // new Marker({color: "#FF0000"})
      //   .setLngLat([21.0122,52.2297])
      //   .addTo(map.value);

      zdrofits.forEach(zdrofits => {
        new Marker({color: "#055ccf"})
          .setLngLat([zdrofits.lng, zdrofits.lat])
          .setPopup(
            new Popup({ offset: 25 })
          .setHTML(`<h3>${zdrofits.nazwa}</h3><p>${zdrofits.adres}</p>`)
        )
        .addTo(map.value);
      });
    }),
    onUnmounted(() => {
      map.value?.remove();
    })

    return {
      map, mapContainer
    };
  }
};
</script>


<style scoped>
@import '~maplibre-gl/dist/maplibre-gl.css';

.map-wrap {
  position: relative;
  width: 100%;
  height: calc(100vh - 77px); /* calculate height of the screen minus the heading */
}

.map {
  position: absolute;
  width: 100%;
  height: 100%;
}

.watermark {
  position: absolute;
  left: 10px;
  bottom: 10px;
  z-index: 999;
}
</style>
