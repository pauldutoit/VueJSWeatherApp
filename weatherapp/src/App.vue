<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm': ''">
<main>
  <div class="search-box">
    <input type="text"
      class="search-bar"
      placeholder="Recherche..."
      v-model="query"
      @keypress.enter="fetchWeather"
    />
  </div>
  <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
    <div class="location-box">
      <div class="location">
        {{ weather.name }}, {{ weather.sys.country }}
      </div>
      <div class="date"> 
        {{ dateBuilder() }}
      </div>
    </div>
    <div class="weather-box">
    <div class="temp"><span>{{ Math.floor(weather.main.temp) }}</span>°C</div>
    <div class="weather">{{ weather.weather[0].main }}</div>
    </div>
  </div>
</main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data (){
    return {
     api_key: 'Your api key',
     base_url: 'https://api.openweathermap.org/data/2.5/',
     query: '',
     weather: {} 
    }
  },
  methods: {
    fetchWeather(){
        fetch(`${this.base_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          //console.log(res.json())
          return res.json();
        }).then(this.setResults);
    },
    setResults(results){
      this.weather = results;
    },
    dateBuilder(){
      let d = new Date();
      let months = ['Janvier', 'Février', 'Mars',
       'Avril', 'Mai', 'Juin', 'Juillet', 'Aout',
       'Septembre', 'Octobre', 'Novembre', 'Décembre'];
      let days = ['Lundi', 'Mardi', 'Mercredi', 'Jeudi',
       'Vendredi', 'Samedi', 'Dimanche'];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();      

      return `${day} ${date} ${month} ${year}`
    }
  }
}
</script>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
font-family: Optima, sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25),  rgba(0, 0, 0, 0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #c0c0c0;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none; 
  background: none;

  background-color: rgba(255, 255, 255, 0.5);
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.3);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.6);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.3);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #FFF;
  font-size: 15px;
  font-weight: 100;
  text-align: center;
  font-style: italic;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  color: #FFF;
  display: inline-block;
  padding: 10px 25px;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.15);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #FFF;
  font-size: 40px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);


}


/*
1ere partie : 
I.Etudes de marché 
analyse environnement éco
définir la mission et la vision de l’entreprise
Fixer l’offre proposée -> laser game +/- définir le concept
fixer la stratégie d’entreprise (canvas stratégique de secteur)
2eme partie:
II.Strategie de l’ocean bleu
III.SWOT
IV.Chaine de force de porter
3eme partie
V.Business model canva 
1/ le financement en entreprise
2/ la proposition de valeur
3/ le segment de clientèle visée
4/ la structure des coûts (5P)
*/




</style>
