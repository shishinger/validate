<template>
  <section class="section">
    <h2 class="subttile">Адрес</h2>
    <div class="block">
      <div class="block__item block__item--third">
        <label class="label" for>Индекс</label>
        <input
          class="input input--num"
          type="number"
          placeholder="Индекс"
          name="index"
          id="index"
        />
      </div>
      <div class="block__item block__item--third">
        <label class="label" for>Страна</label>
        <input
          class="input"
          type="text"
          placeholder="Страна"
          name="country"
          id="country"
        />
      </div>
      <div class="block__item block__item--third">
        <label class="label" for>Область</label>
        <input
          class="input"
          type="text"
          placeholder="Область"
          name="region"
          id="region"
        />
      </div>
    </div>
    <div class="block">
      <div
        :class="{ error: v$.city.$error }"
        class="block__item block__item--third"
      >
        <label class="label required" for>Город</label>
        <input
          class="input"
          v-model="city"
          type="text"
          placeholder="Город"
          name="city"
          id="city"
        />
        <div
          class="error__message"
          v-if="v$.city.$error"
        >{{ v$.city.required.$message }}</div>
      </div>
      <div class="block__item block__item--third">
        <label class="label" for="street">Улица</label>
        <input
          class="input"
          type="text"
          placeholder="Улица"
          name="street"
          id="street"
        />
      </div>
      <div class="block__item block__item--third">
        <label class="label" for="street">Дом</label>
        <input
          class="input input--number"
          type="number"
          placeholder="Дом"
          name="house"
          id="house"
        />
      </div>
    </div>
  </section>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, helpers } from "@vuelidate/validators";

export default {
  name: "Address",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      city: "",
    };
  },
  validations() {
    return {
      city: {
        required: helpers.withMessage("Введите город", required),
      },
    };
  },
};
</script>

<style>
</style>