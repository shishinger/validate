<template>
  <section class="section">
    <h2 class="subtitle">Основные данные</h2>
    <fieldset class="block">
      <legend class="legend">ФИО</legend>
      <div :class="{}" class="block__item block__item--third">
        <TextRequired v-model:name="surname" section="Фамилия" id="surname" />
        <div class="error__message">{{ }}</div>
      </div>
      <div :class="{}" class="block__item block__item--third">
        <TextRequired v-model:name="name" section="Имя" id="name" />
        <div class="error__message">{{ }}</div>
      </div>
      <div class="block__item block__item--third">
        <label class="label" for="patronym">Отчество</label>
        <input class="input" type="text" placeholder="Отчество" name="patronym" id="patronym" />
      </div>
    </fieldset>
    <fieldset :class="{}" class="block">
      <legend class="legend">Дата рождения</legend>
      <DateSelect
        v-model:day="birthDay"
        v-model:month="birthMonth"
        v-model:year="birthYear"
        section="рождения"
        id="birth"
      />
      <div class="error__message self">{{ }}</div>
    </fieldset>
    <div class="block">
      <p class="legend">Личная информация</p>
      <div :class="{}" class="block__item block__item--third">
        <div>
          <label class="label required" for="tel">Номер телефона</label>
          <input
            class="input"
            type="tel"
            v-model.number="tel"
            placeholder="Номер телефона"
            name="tel"
            id="tel"
            maxlength="11"
          />
          <div class="error__message">{{ }}</div>
        </div>
      </div>
      <fieldset class="block__item block__item--third radio">
        <legend class="label">Пол</legend>
        <input class="radio__btn hidden" type="radio" name="sex" id="male" checked />
        <label class="radio__label" for="male">Мужской</label>
        <input class="radio__btn hidden" type="radio" name="sex" id="female" />
        <label class="radio__label" for="female">Женский</label>
      </fieldset>
      <div class="block__item block__item--third">
        <label class="label" for="doctor">Лечащий врач</label>
        <select class="select" name="doctor" id="doctor">
          <option value disabled>Лечащий врач</option>
          <option :value="doctor" v-for="doctor in doctors" :key="doctor">{{ doctor }}</option>
        </select>
      </div>
    </div>
    <div class="block">
      <div :class="{}" class="block__item block__item--half">
        <label class="label required" for="clientGroup">Группа клиентов</label>
        <select
          class="select mul"
          name="clientGroup"
          id="clientGroup"
          v-model="clientGroup"
          multiple
        >
          <option :value="group" v-for="group in groups" :key="group">{{ group }}</option>
        </select>
        <div class="error__message">{{ }}</div>
      </div>
      <div class="block__item block__item--third">
        <input class="checkbox" type="checkbox" name="noSMS" id="noSMS" value="noSMS" />
        <label class="legend" for="noSMS">Не отправлять СМС</label>
      </div>
    </div>
  </section>
</template>

<script>
import DateSelect from './DateSelect.vue';
import TextRequired from "./TextRequired.vue";

export default {
  components: { DateSelect, TextRequired },
  name: "Main",
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
