<template>
	<fieldset class="block">
		<legend class="legend required">Дата {{ section }}</legend>
		<div :class="{ error: v$.day.$error }" class="block__item">
			<select
				@blur="v$.day.$touch"
				class="select"
				:name="name + 'Day'"
				:id="name + 'Day'"
				v-model.number="day"
			>
				<option value disabled>День</option>
				<option
					v-for="dayValue in getDay"
					:key="dayValue"
					:value="dayValue"
				>{{ dayValue }}</option>
			</select>
			<label class="label" :for="name + 'Day'">День {{ section }}</label>
			<div
				class="error__message"
				v-if="v$.day.$error"
			>{{ v$.day.required.$message }}</div>
		</div>
		<div :class="{ error: v$.month.$error }" class="block__item">
			<label class="label" :for="name + 'Month'">Месяц {{ section }}</label>
			<select
				@blur="v$.month.$touch"
				class="select"
				v-model="month"
				:name="name + 'Month'"
				:id="name + 'Month'"
			>
				<option value disabled>Месяц</option>
				<option
					v-for="monthValue in monthList"
					:key="monthValue"
					:value="monthValue"
				>{{ monthValue }}</option>
			</select>
			<div
				class="error__message"
				v-if="v$.month.$error"
			>{{ v$.month.required.$message }}</div>
		</div>
		<div :class="{ error: v$.year.$error }" class="block__item">
			<label class="label" :for="name + 'Year'">Год {{ section }}</label>
			<select
				@blur="v$.year.$touch"
				class="select"
				:name="name + 'Year'"
				:id="name + 'Year'"
				v-model.number="year"
			>
				<option value disabled>Год рождения</option>
				<option
					:value="yearValue + (yearStart - yearRange) + 1"
					v-for="yearValue in yearList"
					:key="yearValue"
				>{{ yearValue + (yearStart - yearRange) + 1 }}</option>
			</select>
			<div
				class="error__message"
				v-if="v$.year.$error"
			>{{ v$.year.required.$message }}</div>
		</div>
	</fieldset>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, helpers } from "@vuelidate/validators";

export default {
	name: "DateSelect",
	setup() {
		return {
			v$: useVuelidate(),
		};
	},
	data() {
		return {
			day: "",
			month: "",
			year: "",
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
	props: {
		section: String,
		name: String,
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
	validations() {
		return {
			day: {
				required: helpers.withMessage(`Введите день ${this.section}`, required),
			},
			month: {
				required: helpers.withMessage(`Введите месяц ${this.section}`, required),
			},
			year: {
				required: helpers.withMessage(`Введите год ${this.section}`, required),
			},
		};
	},
};
</script>

<style>
</style>