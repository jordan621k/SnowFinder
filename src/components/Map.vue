<template>
  <div>
    <v-btn class="pink white--text" @click="Homeview">HomeView</v-btn>
    <v-btn class="pink white--text" @click="HunterMtview">GO hunter!</v-btn>
    <v-btn class="pink white--text" @click="MtCreekview">GO Mtcreek!</v-btn>
    <v-btn class="pink white--text" @click="CamalBackview">GO Camalback!</v-btn>
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
    this.markers = []
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
      var huntermtmarker = L.marker(this.huntermtll,{title:"marker_hunter"}).addTo(this.map).bindPopup('Hunter Mt')
      this.markers.push(huntermtmarker)
      var mtcreekmarker = L.marker(this.mtcreekll,{title:"marker_creek"}).addTo(this.map).bindPopup('Mt Creek')
      this.markers.push(mtcreekmarker)
      var Camelbackmarker = L.marker(this.camalbackll,{title:"marker_camel"}).addTo(this.map).bindPopup('Camelback')
      this.markers.push(Camelbackmarker)
    },
    Homeview() {
      this.map.flyTo(this.homeviewll, this.homezoom)
    },
    HunterMtview() {
      this.map.flyTo(this.huntermtll, this.flyzoom)
      for (var i in this.markers){
        var markerID = this.markers[i].options.title
        if (markerID == "marker_hunter"){
            this.markers[i].openPopup()
        }
      }
    },
    MtCreekview() {
      this.map.flyTo(this.mtcreekll, this.flyzoom)
      for (var i in this.markers){
        var markerID = this.markers[i].options.title
        if (markerID == "marker_creek"){
            this.markers[i].openPopup()
        }
      }
    },
    CamalBackview() {
      this.map.flyTo(this.camalbackll, this.flyzoom)
      for (var i in this.markers){
        var markerID = this.markers[i].options.title
        if (markerID == "marker_camel"){
            this.markers[i].openPopup()
        }
      }
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
