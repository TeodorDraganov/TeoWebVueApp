<script>
import axios from 'axios';

export default {
  data(){
    return{
      city: "",
      error: "",
      info: null
    }
  },
  computed: {
    cityName() {
      return "''" + this.city + "''"
    },
    showTemp(){
      return "Temperature: " + this.info.main.temp
    },
    showFeelsLike(){
      return "Feels like: " + this.info.main.feels_like
    },
    showMinTemp(){
      return "Minimal Temperature: " + this.info.main.temp_min
    },
    ShowMaxTemp(){
      return "Maximal temperature: " + this.info.main.temp_max
    },

  },
  methods: {
    getWeather (){
      if(this.city.trim().length < 2){
        this.error =" Need name more than 1 symbols"
        return false
      }

      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid={enter your API key from Open WeatherMap}`)
        .then(res => (this.info = res.data) )
    }
  }
}
</script>

<template>
 <div class="wraper">
  <h1>Weather app </h1>
  <p>See weather  {{ city == "" ? "in your town" : cityName}}</p>
  <input type="text" v-model="city" placeholder="Enter your town">
  <button v-if="city != '' " @click="getWeather()">get a weather</button>
  <button disabled v-else="city != '' ">enter a name of city</button>

  <p class="error">{{ error }}</p>

  <div v-if="info !=null">
    <p>{{ showTemp }}</p>
    <p>{{ showFeelsLike }}</p>
    <p>{{ showMinTemp }}</p>
    <p>{{ ShowMaxTemp }}</p>
  </div>

 </div>
</template>

<style scoped>
.error {
  color: #d03939;
}

.wraper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24 ;
  text-align: center;
  color: #fff
}

.wraper h1{
  margin-top: 50px;
}

.wraper p {
  margin-top: 20px;
}

.wraper input {
  margin-top: 30px;
  background: transparent ;
  border: 0;
  border-bottom: 2px solid #110813 ;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wraper input:focus {
  border-bottom-color: #6e2d7d;
}


.wraper button:disabled{
  background: #6d5b25;
  cursor: not-allowed;

}

.wraper button{
  background: #010115;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #de9c5e;
  padding: 10px 15px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wraper button:hover{
  transform: scale(1.1) translateY(-5px);
}
</style>
