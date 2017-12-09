<template>
  <div class="google-map" :id="mapName"></div>
</template>

<script>
export default {
  name: 'google-map',
  props: ['name'],
  data: function () {
    return {
      mapName: this.name + '-map',
      markerCoordinates: [{
        latitude: 41.885080,
        longitude: -87.624135
      }, {
        latitude: 41.831008,
        longitude: -88.010101
      }, {
        latitude: 42.139287,
        longitude: -88.056793
      }, {
        latitude: 42.002685,
        longitude: -86.392365
      }],
      map: null,
      bounds: null,
      markers: []
    }
  },
  mounted: function () {
    this.bounds = new window.google.maps.LatLngBounds()
    const element = document.getElementById(this.mapName)
    const mapCentre = this.markerCoordinates[0]
    const options = {
      center: new window.google.maps.LatLng(mapCentre.latitude, mapCentre.longitude)
    }
    this.map = new window.google.maps.Map(element, options)
    this.markerCoordinates.forEach((coord) => {
      const position = new window.google.maps.LatLng(coord.latitude, coord.longitude)
      const marker = new window.google.maps.Marker({
        position,
        map: this.map
      })
      this.markers.push(marker)
      this.map.fitBounds(this.bounds.extend(position))
    })
  }
}
</script>

<style scoped>
.google-map {
  width: 800px;
  height: 600px;
  margin: 0 auto;
  background: gray;
}
</style>