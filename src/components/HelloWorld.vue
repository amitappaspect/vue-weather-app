<template>
	<div class="container">
    <div class="m-3">
      <input v-model="city_name" type="text" class="w-2/12 mx-auto h-auto rounded border-1 p-3 shodow" placeholder="City">
      <button class="w-1/12 h-auto rounded border-1 py-3 ml-2 text-white font-bold bg-gradient-to-r from-blue-300 via-blue-400 to-pink-500 shodow" v-on:click="getCurrentWeather">Search</button>
    </div>
		<div class="bg-white	 rounded-lg shadow-lg sm:w-10/12	 md:w-3/12 mx-auto h-auto p-3">
			<h2 class="font-bold">Today in {{weather.name}}</h2><br/>
      <span class="font-semibold text-gray">{{ new Date().toLocaleDateString() }}</span>
      <img :src="'https://openweathermap.org/img/wn/'+weather.weather[0].icon+'@2x.png'" class="img-fluid mx-auto"><br/>
      <h1 class="font-extrabold	">{{weather.weather[0].main}}</h1><br/>
      <div class="text-left	mx-auto p-3">
        <div class="bg-gray-100 shadow text-gray-700 p-2 mt-1 align-middle rounded hover:shadow-lg hover:bg-gray-200 hover:text-black">
          <span><img src="https://img.icons8.com/nolan/64/thermometer.png" class="w-12 h-12 float-left"/> Temprature: {{weather.main.temp}} °C</span><br/><br/>
        </div>
        <div class="bg-gray-100 shadow text-gray-700 p-2 mt-1 align-middle rounded hover:shadow-lg hover:bg-gray-200 hover:text-black">
        <span><img src="https://img.icons8.com/nolan/64/partly-cloudy-day.png" class="w-12 h-12 float-left"/> humidity: {{weather.main.humidity}}%</span><br/><br/>
        </div>
        <div class="bg-gray-100 shadow text-gray-700 p-2 mt-1 align-middle rounded hover:shadow-lg hover:bg-gray-200 hover:text-black">
        <span><img src="https://img.icons8.com/nolan/64/wind.png" class="w-12 h-12 float-left"/> Wind Speed: {{weather.wind.speed}}%</span><br/><br/>
        </div>
      </div>
		</div>
	</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    city: String
  },
  data(){
	return {
    city_name:this.city,
    weather:'',
		api_key:'a42abc7db67c188a58c94b19cb514e68',
	}
  },
  mounted(){
    this.getCurrentWeather();
  },
  methods:{
	async getCurrentWeather(){
		this.axios.get('https://api.openweathermap.org/data/2.5/weather?q='+this.city_name+'&units=metric&appid='+this.api_key).then((response) => {
			console.log(response.data)
      this.weather = response.data;
		})
	}
  }
}
</script>