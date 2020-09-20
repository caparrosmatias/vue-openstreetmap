<template>
  <div>
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Mapa interactivo</h1>
          <h2 class="subtitle">Desarrollado en Vue.js</h2>
        </div>
      </div>
    </section>
    <br>
    <br>

    <div class="container">
      <div class="columns">
        <div class="column">
          <div style="height: 200px overflow: auto;">
            <div class="tile">
              <article class="tile is-child box">
                <p class="subtitle">#1 Departamento</p>
                <p>Avenida Mitre 1545</p>
                <p>Departamento completo, 2 habitaciones</p>
                <a href="url">Más info</a>
              </article>
            </div>
            <br>
            <div class="tile">
              <article class="tile is-child box">
                <p class="subtitle">#2 Habitación privada</p>
                <p>Calle Sarmiento 122</p>
                <p>Habitación privada en casa de familia, ideal estudiantes</p>
                <a href="url">Más info</a>
              </article>
            </div>
            <br>
            <div class="tile">
              <article class="tile is-child box">
                <p class="subtitle">#3 Habitación compartida</p>
                <p>Calle Rivadavia 341</p>
                <p>Habitación compartida entre 6 estudiantes. Hostel.</p>
                <a href="url">Más info</a>
              </article>
            </div>Alquileres disponibles en la zona de Mendoza
            <p>El primer marcador está en: {{ alquiler0.lat }}, {{ alquiler0.lng }}</p>
            <p>El segundo marcador está en: {{ alquiler1.lat }}, {{ alquiler1.lng }}</p>
            <p>El tercer marcador está en: {{ alquiler2.lat }}, {{ alquiler2.lng }}</p>
            <p>Centro: {{ currentCenter }} / Zoom: {{ currentZoom }}</p>
            <button @click="showLongText">Popup 1</button>
            <button @click="showMap = !showMap">Activa/Desactiva</button>
          </div>
        </div>
        <div class="column">
          <l-map
            v-if="showMap"
            :zoom="zoom"
            :center="center"
            :options="mapOptions"
            style="height: 500px"
            @update:center="centerUpdate"
            @update:zoom="zoomUpdate"
          >
            <l-tile-layer :url="url" :attribution="attribution"/>
            <l-marker :lat-lng="alquiler0">
              <l-popup>
                <div @click="innerClick">Calle Sarmiento
                  <p v-show="showParagraph">Parrafo largo.</p>
                </div>
              </l-popup>
            </l-marker>
            <l-marker :lat-lng="alquiler1">
              <l-popup>
                <div @click="innerClick">Calle Mitre
                  <p v-show="showParagraph">Parrafo largo.</p>
                </div>
              </l-popup>
            </l-marker>
            <l-marker :lat-lng="alquiler2">
              <l-tooltip :options="{ permanent: true, interactive: true }">
                <div @click="innerClick">Plaza Independencia
                  <p v-show="showParagraph">Parrafo largo.</p>
                </div>
              </l-tooltip>
            </l-marker>
          </l-map>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LPopup, LTooltip } from "vue2-leaflet";

export default {
  name: "Example",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LTooltip
  },
  data() {
    return {
      zoom: 15,
      center: latLng(-32.89012, -68.8424),
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      alquiler0: latLng(-32.889194, -68.845691),
      alquiler1: latLng(-32.891295, -68.845066),
      alquiler2: latLng(-32.889845, -68.844076),
      currentZoom: 1,
      currentCenter: latLng(-32.89012, -68.8424),
      showParagraph: false,
      mapOptions: {
        zoomSnap: 0.5
      },
      showMap: true
    };
  },
  methods: {
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    showLongText() {
      this.showParagraph = !this.showParagraph;
    },
    innerClick() {
      alert("Click!");
    }
  }
};
</script>

<style>
</style>
