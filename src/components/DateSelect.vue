<template>
  <div class="block__item block__item--third">
    <label class="label" :for="id + 'Day'">День {{ section }}</label>
    <select
      class="select"
      :name="id + 'Day'"
      :id="id + 'Day'"
      @click="$emit('update:day', $event.target.value)"
      :value="day"
    >
      <option value disabled>День</option>
      <option
        v-for="dayValue in getDay"
        :key="dayValue"
        :value="dayValue"
      >{{ dayValue }}</option>
    </select>
  </div>
  <div class="block__item block__item--third">
    <label class="label" :for="id + 'Month'">Месяц {{ section }}</label>
    <select
      class="select"
      @click="$emit('update:month', $event.target.value)"
      :value="month"
      :name="id + 'Month'"
      :id="id + 'Month'"
    >
      <option value disabled>Месяц</option>
      <option
        v-for="monthValue in monthList"
        :key="monthValue"
        :value="monthValue"
      >{{ monthValue }}</option>
    </select>
  </div>
  <div class="block__item block__item--third">
    <label class="label" :for="id + 'Year'">Год {{ section }}</label>
    <select
      class="select"
      @click="$emit('update:year', $event.target.value)"
      :value="year"
      :name="id + 'Year'"
      :id="id + 'Year'"
    >
      <option value disabled>Год</option>
      <option
        :value="yearValue + (yearStart - yearRange) + 1"
        v-for="yearValue in yearList"
        :key="yearValue"
      >{{ yearValue + (yearStart - yearRange) + 1 }}</option>
    </select>
  </div>
</template>

<script setup>
defineProps({
  day: { type: String },
  month: { type: String },
  year: { type: String },
  section: { type: String },
  id: { type: String }
});
defineEmits([
  "update:day",
  "update:month",
  "update:year"
])
</script>

<script>
export default {
  data() {
    return {
      monthList: [
        "Январь",
        "Февраль",
        "Март",
        "Апрель",
        "Май",
        "Июнь",
        "Июль",
        "Август",
        "Сентябрь",
        "Октябрь",
        "Ноябрь",
        "Декабрь",
      ],
      yearRange: 100,
      yearList: [...Array(100).keys()].reverse(),
      yearStart: new Date().getFullYear(),
    };
  },
  computed: {
    getDay() {
      switch (this.month) {
        case "Февраль":
          return 28;
        case "Январь":
        case "Март":
        case "Май":
        case "Июль":
        case "Август":
        case "Октябрь":
        case "Декабрь":
          return 31;
        default:
          return 30;
      }
    },
  },
};
</script>


<style>
</style>