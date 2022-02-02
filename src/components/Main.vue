<template>
  <section class="section">
    <h2 class="subtitle">Основные данные</h2>
    <fieldset class="block">
      <legend class="legend">ФИО</legend>
      <div
        :class="{ error: v$.surname.$error }"
        class="block__item block__item--third"
      >
        <TextRequired v-model:name="surname" section="Фамилия" id="surname" />
        <div
          class="error__message"
          v-if="v$.surname.$error"
        >{{ v$.surname.required.$message }}</div>
      </div>
      <div
        :class="{ error: v$.name.$error }"
        class="block__item block__item--third"
      >
        <TextRequired v-model:name="name" section="Имя" id="name" />
        <div
          class="error__message"
          v-if="v$.name.$error"
        >{{ v$.name.required.$message }}</div>
      </div>
      <div class="block__item block__item--third">
        <label class="label" for="patronym">Отчество</label>
        <input
          class="input"
          type="text"
          placeholder="Отчество"
          name="patronym"
          id="patronym"
        />
      </div>
    </fieldset>
    <fieldset
      :class="{ error: v$.birthDay.$error || v$.birthMonth.$error || v$.birthYear.$error }"
      class="block"
    >
      <legend class="legend">Дата рождения</legend>
      <DateSelect
        v-model:day="birthDay"
        v-model:month="birthMonth"
        v-model:year="birthYear"
        section="рождения"
        id="birth"
      />
      <div
        class="error__message self"
        v-if="v$.birthDay.$error || v$.birthMonth.$error || v$.birthYear.$error"
      >{{ v$.birthDay.required.$message }}</div>
    </fieldset>
    <div class="block">
      <p class="legend">Личная информация</p>
      <div
        :class="{ error: v$.tel.$error }"
        class="block__item block__item--third"
      >
        <div>
          <label class="label required" for="tel">Номер телефона</label>
          <input
            @blur="v$.tel.$touch"
            class="input"
            type="tel"
            v-model.number="tel"
            placeholder="Номер телефона"
            name="tel"
            id="tel"
            maxlength="11"
          />
          <div
            class="error__message"
            v-if="v$.tel.$error"
          >{{ v$.tel.required.$message }}</div>
        </div>
      </div>
      <fieldset class="block__item block__item--third radio">
        <legend class="label">Пол</legend>
        <input
          class="radio__btn hidden"
          type="radio"
          name="sex"
          id="male"
          checked
        />
        <label class="radio__label" for="male">Мужской</label>
        <input class="radio__btn hidden" type="radio" name="sex" id="female" />
        <label class="radio__label" for="female">Женский</label>
      </fieldset>
      <div class="block__item block__item--third">
        <label class="label" for="doctor">Лечащий врач</label>
        <select class="select" name="doctor" id="doctor">
          <option value disabled>Лечащий врач</option>
          <option
            :value="doctor"
            v-for="doctor in doctors"
            :key="doctor"
          >{{ doctor }}</option>
        </select>
      </div>
    </div>
    <div class="block">
      <div
        :class="{ error: v$.clientGroup.$error }"
        class="block__item block__item--half"
      >
        <label class="label required" for="clientGroup">Группа клиентов</label>
        <select
          @blur="v$.clientGroup.$touch"
          class="select mul"
          name="clientGroup"
          id="clientGroup"
          v-model="clientGroup"
          multiple
        >
          <option
            :value="group"
            v-for="group in groups"
            :key="group"
          >{{ group }}</option>
        </select>
        <div
          class="error__message"
          v-if="v$.clientGroup.$error"
        >{{ v$.clientGroup.required.$message }}</div>
      </div>
      <div class="block__item block__item--third">
        <input
          class="checkbox"
          type="checkbox"
          name="noSMS"
          id="noSMS"
          value="noSMS"
        />
        <label class="legend" for="noSMS">Не отправлять СМС</label>
      </div>
    </div>
  </section>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, helpers } from "@vuelidate/validators";
import DateSelect from './DateSelect.vue';
import TextRequired from "./TextRequired.vue";

export default {
  components: { DateSelect, TextRequired },
  name: "Main",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      surname: "",
      name: "",
      birthDay: "",
      birthMonth: "",
      birthYear: "",
      tel: "7",
      clientGroup: [],
      birthMessage: "Введите дату рождения",
      groups: ["VIP", "Проблемные", "ОМС"],
      doctors: ["Иванов", "Захаров", "Чернышева"],
    };
  },
  validations() {
    return {
      surname: {
        required: helpers.withMessage("Введите фамилию", required),
      },
      name: {
        required: helpers.withMessage("Введите имя", required),
      },
      tel: {
        required: helpers.withMessage(
          "Номер должен начинаться с 7 и содержать 11 цифр",
          required
        ),
        validTel: helpers.regex(/[7]\d{10}$/m),
      },
      clientGroup: {
        required: helpers.withMessage("Выберите группу", required),
      },
      birthDay: {
        required: helpers.withMessage(this.birthMessage, required)
      },
      birthMonth: { required: helpers.withMessage(this.birthMessage, required) },
      birthYear: { required: helpers.withMessage(this.birthMessage, required) },
    };
  },
  methods: {
    async submitForm() {
      const isFormCorrect = await this.v$.$validate();

      if (!isFormCorrect) {
        console.log(this.v$.day);
      }
      // actually submit form
    },
  },
};
</script>
<style lang="scss">
@import "../style/variables.scss";

.radio,
.radio__label {
  cursor: pointer;
}
.radio {
  @extend %df_cc;
  &__btn:checked + &__label {
    border-color: $accent;
  }
  &__label {
    padding: 0.5em 1em;
    border: 1px solid transparent;
    transition: border-color ease-in-out 0.3s;
    &:nth-of-type(1) {
      border-top-left-radius: 1em;
      border-bottom-left-radius: 1em;
    }
    &:nth-of-type(2) {
      border-top-right-radius: 1em;
      border-bottom-right-radius: 1em;
    }
  }
}
.checkbox {
  margin-right: 0.2em;
}
</style>
