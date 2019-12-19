<template>
  <div>
    <v-btn class="pink white--text" @click="HunterMtview" large>GO!</v-btn>
    <div id="map" ref="mapElement">
    </div>
  </div>
</template>

<script>
import L from 'leaflet';

export default {
  name: "Map",
  mounted() {
    this.initMap();
  },
  data() {
    return {
      huntermtview: false,
      mtcreekview: false,
      camalbackview: false,
    };
  },
  created() {
  },
  watch: {
    huntermtview: {
      immediate: true,
      handler() {
        this.HunterMtview()
      }
    }
  },
  methods: {
    initMap() {
      let map = L.map(this.$refs['mapElement']).setView([41.17878, -74.53104], 7);
      L.tileLayer('https://maps.wikimedia.org/osm-intl/{z}/{x}/{y}{r}.png', {
        attribution: '<a href="https://wikimediafoundation.org/wiki/Maps_Terms_of_Use">Wikimedia</a>',
        minZoom: 1,
        maxZoom: 19
      }).addTo(map);

      L.marker([42.204518, -74.210525]).addTo(map)
        .bindPopup('Hunter Mt')
        .openPopup();
      
      L.marker([41.17878,-74.53104]).addTo(map)
        .bindPopup('Mt Creek')
        .openPopup();
      
      L.marker([41.053379,-75.354263]).addTo(map)
        .bindPopup('Camalback')
        .openPopup();
    },
    HunterMtview() {
      console.log("xxx")
      L.map(this.$refs['mapElement']).setView([42.204518, -74.210525], 13);
    }
  }
}
</script>

<style scoped>
#map {
  position: fixed;
  bottom: 1;
  right: 0;
  border: 3px solid #73AD21;
  width: 50%;
  height: 50%;
}
</style>
