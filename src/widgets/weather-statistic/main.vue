<template>
  <div class="weather-statistic">
    <div class="weather-statistic--head">
      <div class="weather-statistic--head-container container">
        TODO: Date Pick
      </div>
    </div>
    <div class="weather-statistic--body container">
      <Card class="card--white cart--split">
        <Card>
          осадки
        </Card>
        <Card>
          Облачность
        </Card>
      </Card>
      <Card class="card--white">
        Динамика
      </Card>
    </div>
  </div>
</template>
<script lang="ts" setup>
import Card from '@/shared/ui/Card/index.vue';

defineOptions({
  name: 'WeatherStatistics',
});

enum EStatus {
  'pending',
}

const status = ref(2);


const fetchWeatherStatistic = () => {
  import {fetchWeatherApi} from 'openmeteo';

  const params = {
    "latitude": 52.52,
    "longitude": 13.41,
    "current": ["precipitation", "cloud_cover"],
    "hourly": "temperature_2m",
    "wind_speed_unit": "ms",
    "timeformat": "unixtime",
    "forecast_days": 14
  };

  const url = "https://api.open-meteo.com/v1/forecast";

  const responses = await fetchWeatherApi(url, params);

// Helper function to form time ranges
  const range = (start: number, stop: number, step: number) =>
    Array.from({length: (stop - start) / step}, (_, i) => start + i * step);

// Process first location. Add a for-loop for multiple locations or weather models
  const response = responses[0];

// Attributes for timezone and location
  const utcOffsetSeconds = response.utcOffsetSeconds();
  const timezone = response.timezone();
  const timezoneAbbreviation = response.timezoneAbbreviation();
  const latitude = response.latitude();
  const longitude = response.longitude();

  const current = response.current()!;
  const hourly = response.hourly()!;

// Note: The order of weather variables in the URL query and the indices below need to match!
  const weatherData = {
    current: {
      time: new Date((Number(current.time()) + utcOffsetSeconds) * 1000),
      precipitation: current.variables(0)!.value(),
      cloudCover: current.variables(1)!.value(),
    },
    hourly: {
      time: range(Number(hourly.time()), Number(hourly.timeEnd()), hourly.interval()).map(
        (t) => new Date((t + utcOffsetSeconds) * 1000)
      ),
      temperature2m: hourly.variables(0)!.valuesArray()!,
    },

  };

// `weatherData` now contains a simple structure with arrays for datetime and weather data
  for (let i = 0; i < weatherData.hourly.time.length; i++) {
    console.log(
      weatherData.hourly.time[i].toISOString(),
      weatherData.hourly.temperature2m[i]
    );
  }

}

</script>
<style scoped>
.weather-statistic--head {
  border-bottom: 1px solid #B3D1FE;
}

.weather-statistic--head-container {
  padding: 16px;
}

.weather-statistic--body {
  display: flex;
  flex-direction: column;
  row-gap: 20px;
  padding: 16px;
}

/* todo удалить этот костыль */
.cart--split {
  display: flex;
  flex-direction: row;
  column-gap: 16px;
}
</style>
