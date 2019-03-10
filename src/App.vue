<template>
	<div id="app">
		<div class="container">
			<app-select-country :countries="countries" @countryWasChoose="setCities"></app-select-country>
			<app-select-city :selectedCitiesFromParent="cities"></app-select-city>			
			<figure :class="setFigureClass(index)" v-for="(item, index) in randomCitiesData" :key="index">
				<i :class="['icon', setWeatherIcon(item.weather[0].main)]"></i>
				<p class="info"><strong>{{item.name}}</strong></p>
				<p class="info">Temperature is: {{item.main.temp}}</p>
			</figure>
		</div>
	</div>
</template>

<script>
import cityList from "./data/city.list.min.json";
import countriesCodes from "./data/countries.iso.codes.json";
import SelectCountry from "./components/SelectCountry.vue";
import SelectCity from "./components/SelectCity.vue";

export default {
	data() {
		return {
			countries: [],
			cities: [],
			randomCitiesData: []
		}
	},
	components: {
		appSelectCountry: SelectCountry,
		appSelectCity: SelectCity
	},
	methods: {
		setCities(country) {
			this.cities = cityList.filter(elem => elem.country === country);
			this.getRandomCities();
		},
		
		getRandomCities() {
			let randomIndex = [];
			for (let i = 0; i < 6; i++) {
				randomIndex.push(Math.floor(Math.random() * (this.cities.length - 1) + 1));
			}

			let randomCities = [];
			randomIndex.forEach( elem => {
				randomCities.push(this.cities[elem].id);
			});
			randomCities = randomCities.join();

			this.$http.get(`https://api.openweathermap.org/data/2.5/group?id=${randomCities}&units=metric&appid=e642e0062bffd9aca2bf891e4d8646a2`)
				.then( response => response.json())
				.then( data => this.randomCitiesData = data.list);
		},

		setCountries () {
			let set = new Set();
			cityList.forEach( elem => set.add(elem.country));
			set.forEach(elem => {
				if (elem) {
					const currentItem = countriesCodes.find(item => item['alpha-2'] === elem);

					if (currentItem) {
						this.countries.push({
							value: elem,
							label: currentItem.name
						});
					}
				}
			});
		},
		setWeatherIcon (weather) {
			if (weather === "Rain" || weather === "Thunderstorm" || weather === "Drizzle" || weather === "Snow") {
				return "icon-rain";
			} else if (weather === "Clouds") {
				return "icon-simple-cloud";
			} else if (weather === "Atmosphere" || weather === "Clear") {
				return "icon-sun-cloud";
			}
		},
		setFigureClass (i) {
			switch (i) {
				case 0:
					return 'purple';
					break;
				case 1:
					return "lightgreen";
					break;
				case 2:
					return "rose";
					break;
				case 3: 
					return "mustard";
					break;
				case 4:
					return "blue";
					break;
				case 5:
					return "darker-blue";
					break;
			}
		}
	},

	mounted() {
		this.setCountries();
	}
}
</script>

<style lang="scss">
@import "./styles/icons.scss";

#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

.container {
	display: flex;
	flex-wrap: wrap;
	align-content: center;
	justify-content: center;
	width: 800px;
	height: 600px;
	margin: auto;
	background: url("./images/Layer.png") no-repeat;
}

figure {
	width: 205px;
	margin: 0;
	height: 205px;
	background-color: black;
	box-sizing: border-box;
}

.blue {
	background-color: #06b3db;
}

.lightgreen {
	background-color: #4ed486;
}

.darker-blue {
	background-color: #6139f6;
}

.mustard {
	background-color: #e3b63d;
}

.rose {
	background-color: #dc3d66;
}

.purple {
	background-color: #bd54cd;
}

.info {
	line-height: 0.3;
}

</style>
