<template>
  <div>
    <Form v-on:search="search" />

    <div v-if="this.recentSearches.length > 0">
      {{ result.city }} <br>
      Temp: {{ result.temp }} <br>
      Feels Like: {{ result.feels_like }}
    </div>

    <ul>
      Last 5 searches...
      <li v-for="recent in recentSearches" :key="recent">
        {{ recent }}
      </li>
    </ul>

    <Toast v-if="toast.show" :type="toast.type" :message="toast.message" />
  </div>
</template>

<script>
import Form from "./Form.vue";
import Toast from "./Toast.vue";

export default {
  name: "Home",
  components: { Form, Toast },
  data() {
    return {
      recentSearches: [],
      toast: {
        show: false,
        type: "",
        message: "",
      },
      result: {
        city: "",
        temp: "",
        feels_like: ''
      },
    };
  },
  methods: {
    async search(city) {
      fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=f59095b255decdf854a5ca0e339c7ee4`
      )
        .then((response) => response.json())
        .then((data) => {
          if (data.cod !== 200) {
            this.toast = {
              show: true,
              type: "error",
              message: `The city '${city}' was not found.`,
            };

            setTimeout(() => {
              this.toast.show = false;
            }, 5000);
            return;
          }

          this.result = {
            city: data.name,
            temp: this.tempConvert(data.main.temp).toFixed(1),
            feels_like: this.tempConvert(data.main.feels_like).toFixed(1)
          };
          this.addRecent(city);
        });
    },
    addRecent(city) {
      if (this.recentSearches.length === 5) {
        this.recentSearches.unshift(city);
        this.recentSearches.pop();
      } else {
        this.recentSearches.unshift(city);
      }
    },
    /*
    convert kelvin to celsius
    */
    tempConvert(temp) {
      return temp - 273.15;
    },
  },
};
</script>

<style>
</style>