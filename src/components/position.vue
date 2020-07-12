<template>
<div id="map" style="position: absolute; top: 0; bottom: 0; width: 100%;"></div>
</template>

<script>
var mapboxgl = require('mapbox-gl/dist/mapbox-gl.js')
export default {
  name: 'position',
  props: ['mapdata'],
  components: {
  },
  data () {
    return {
    }
  },
  mounted () {
    this.showmap(this.mapdata)
  },
  methods: {
    showmap (mapdata) {
      console.log('mapdata-', mapdata)
      mapboxgl.accessToken = 'pk.eyJ1IjoiY2hldGFuYm5jb2UiLCJhIjoiY2tjajdkcXU0MHVkbTJzbzNva2owejBqZiJ9.O09c6nyaerdhbVY2qakqkQ'
      var map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/streets-v11',
        center: [77.575288, 13.01221],
        zoom: 10
      })
      map.on('load', function () {
        map.addSource('maine', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'geometry': {
              'type': 'Polygon',
              'coordinates': [mapdata[0]]
            }
          }
        })
        map.addLayer({
          'id': 'maine',
          'type': 'fill',
          'source': 'maine',
          'layout': {},
          'paint': {
            'fill-color': '#088',
            'fill-opacity': 0.9
          }
        })
        map.on('click', 'places', function (e) {
          var coordinates = e.features[0].geometry.coordinates.slice()
          var description = e.features[0].properties.description

          // Ensure that if the map is zoomed out such that multiple
          // copies of the feature are visible, the popup appears
          // over the copy being pointed to.
          while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
            coordinates[0] += e.lngLat.lng > coordinates[0] ? 360 : -360
          }

          new mapboxgl.Popup()
            .setLngLat(coordinates)
            .setHTML(description)
            .addTo(map)
        })

        // Change the cursor to a pointer when the mouse is over the places layer.
        map.on('mouseenter', 'places', function () {
          map.getCanvas().style.cursor = 'pointer'
        })

        // Change it back to a pointer when it leaves.
        map.on('mouseleave', 'places', function () {
          map.getCanvas().style.cursor = ''
        })
      })
    }
  }
}
</script>

<style>
    .mapboxgl-popup {
        max-width: 400px;
        font: 12px/20px 'Helvetica Neue', Arial, Helvetica, sans-serif;
    }
</style>
