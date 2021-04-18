<template>
  <div class="container">
    <h1 class="my-4">App Meteo avec Vue.js</h1>
    <div class="form-group">
      <label for="position">Entrez le nom d'une ville</label>
      <input
        type="text"
        id="position"
        class="form-control"
        v-model="requete"
        @keypress.enter="goMeteo"
      />
      <!-- @keypress.enter : Au click sur entrée, je déclenche l'appel vers l'API -->
    </div>
    <div class="w-75 m-auto " v-if="temps">
      <h3 class="text-center">Position : {{ temps.name }}</h3>
      <div class="card text-center p-5">
        <p class="texte-affichage">Temperature : {{ temps.main.temp }}°</p>
        <p class="texte-affichage">
          Temps : {{ temps.weather[0].description }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Meteo",
  data() {
    return {
      requete: "",
      temps: undefined,
      api_code: "687da8611a212cbc0ca6e58e090589e2",
      url_recherche: "https://api.openweathermap.org/data/2.5/weather?",
    };
  },
  methods: {
    goMeteo() {
      axios
        .get(
          `${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`
        )
        .then((response) => {
          this.temps = response.data;
        });
      this.requete = "";
    },
  },
};
</script>

<style>
.texte-affichage {
  font-size: 20px;
  font-weight: 300;
  line-height: 1.2;
}
</style>
