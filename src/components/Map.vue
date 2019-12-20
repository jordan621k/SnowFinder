<template>
  <div>
    <v-btn class="pink white--text" @click="Homeview">HomeView</v-btn>
    <v-btn class="pink white--text" @click="HunterMtview">GO hunter!</v-btn>
    <v-btn class="pink white--text" @click="MtCreekview">GO Mtcreek!</v-btn>
    <v-btn class="pink white--text" @click="CamalBackview">GO Camalback!</v-btn>
    <v-btn class="pink white--text" @click="Camalpop">Camalback! pop up</v-btn>
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
      map: {},
      huntermtll: [42.204518, -74.210525],
      mtcreekll: [41.17878,-74.53104],
      camalbackll: [41.053379,-75.354263],
      homeviewll: [41.17878, -74.53104],
      homezoom: 7,
      flyzoom: 13,
      huntermarker: [],
    };
  },
  created() {
  },
  watch: {
  },
  methods: {
    initMap() {
      this.map = L.map(this.$refs['mapElement']).setView(this.homeviewll, this.homezoom);
      L.tileLayer('https://maps.wikimedia.org/osm-intl/{z}/{x}/{y}{r}.png', {
        attribution: '<a href="https://wikimediafoundation.org/wiki/Maps_Terms_of_Use">Wikimedia</a>',
        minZoom: 1,
        maxZoom: 19
      }).addTo(this.map);
      var markers = []
      var huntermtmarker = L.marker(this.huntermtll).addTo(this.map).bindPopup('Hunter Mt')
      markers.push(huntermtmarker)
        //.openPopup();
      
      L.marker(this.mtcreekll).addTo(this.map)
        .bindPopup('Mt Creek')
        //.openPopup();
      
      L.marker(this.camalbackll).addTo(this.map)
        .bindPopup('Camalback')
        //.openPopup();
    },
    Homeview() {
      this.map.flyTo(this.homeviewll, this.homezoom)
    },
    HunterMtview() {
      this.map.flyTo(this.huntermtll, this.flyzoom)
    },
    MtCreekview() {
      this.map.flyTo(this.mtcreekll, this.flyzoom)
    },
    CamalBackview() {
      this.map.flyTo(this.camalbackll, this.flyzoom)
    },
    Camalpop() {
      console.log(this.initMap.markers)
      this.markers[this.huntermtmarker].openPopup();
    },
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
