<template>
  <div id="map" ref="mapElement">
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
    };
  },
  created() {
  },
  methods: {
    initMap() {
        let map = L.map(this.$refs['mapElement']).setView([42.204518, -74.210525], 13);
        L.tileLayer('https://maps.wikimedia.org/osm-intl/{z}/{x}/{y}{r}.png', {
          attribution: '<a href="https://wikimediafoundation.org/wiki/Maps_Terms_of_Use">Wikimedia</a>',
          minZoom: 1,
          maxZoom: 19
        }).addTo(map);

        L.marker([42.204518, -74.210525]).addTo(map)
          .bindPopup('A pretty CSS3 popup.<br> Easily customizable.')
          .openPopup();
      }
    }
}
</script>

<style scoped>
#map {
  width: 100%;
  height: 100%;
}
</style>
