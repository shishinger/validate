<template>
	<section class="section">
		<h2 class="subtitle">Паспорт</h2>
		<div class="block">
			<div :class="{}" class="block__item block__item--third">
				<label class="label required" for="docType">Тип документа</label>
				<select class="select" name="docType" id="docType" v-model="doc">
					<option value disabled>Тип</option>
					<option :value="typeValue" v-for="typeValue in docType" :key="typeValue">{{ typeValue }}</option>
				</select>
				<div class="error__message">{{ }}</div>
			</div>
			<div class="block__item block__item--third">
				<label class="label" for="series">Серия</label>
				<input class="input input--number" type="number" placeholder="Серия" name="series" id="series" />
			</div>
			<div class="block__item block__item--third">
				<label class="label" for="number">Номер</label>
				<input class="input input--number" type="number" placeholder="Номер" name="number" id="number" />
			</div>
		</div>
		<div class="block">
			<div class="block__item block__item--full">
				<label class="label" for="receipt">Кем выдан</label>
				<input class="input" type="text" placeholder="Кем выдан" name="receipt" id="receipt" />
			</div>
		</div>
		<fieldset :class="{}" class="block">
			<legend class="legend required" @click="log">Дата получения</legend>
			<DateSelect
				v-model:day="receiptDay"
				v-model:month="receiptMonth"
				v-model:year="receiptYear"
				section="получения"
				id="receipt"
			/>
			<div class="error__message self">{{ }}</div>
		</fieldset>
	</section>
</template>

<script>

import DateSelect from "./DateSelect.vue"
export default {
	name: "Passport",
	components: { DateSelect },
	data() {
		return {
			doc: "",
			receiptDay: "",
			receiptMonth: "",
			receiptYear: "",
			receiptMessage: "Введите дату получения",
			docType: ["Паспорт", "Свидетельство о рождении", "Водительское удостоверение"]
		};
	},
}
</script>

<style>
</style>