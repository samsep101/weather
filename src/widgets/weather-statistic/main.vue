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
import Card from '@/shared/ui/card/index.vue';

defineOptions({
  name: 'WeatherStatistics',
});

enum EStatus {
  'pending',
}

const status = ref(2);


const fetchWeatherStatistic = () => {

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
