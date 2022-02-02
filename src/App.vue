<template>
  <h1 class="title">Регистрация</h1>
  <form class="form">
    <Main />
    <Address />
    <Passport />
    <div class="info">Обязательные поля помечены знаком *</div>
    <button class="btn next" @click.prevent="next">Дальше</button>
  </form>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import Main from "./components/Main.vue";
import Address from "./components/Address.vue";
import Passport from "./components/Passport.vue";

export default {
  name: "App",
  components: {
    Main,
    Address,
    Passport,
  },
  setup() {
    return { v$: useVuelidate({ $touch: blur }) };
  },
  methods: {
    async next() {
      const isFormCorrect = await this.v$.$validate();


      if (!isFormCorrect) {
        console.log(this.v$.$errors);
      }
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Source+Serif+4:ital,wght@0,400;0,500;0,700;0,800;1,400&display=swap");
@import "./style/main.scss";

*,
*::before,
*::after {
  margin: 0;
  border: 0;
  padding: 0;
  box-sizing: border-box;
}
:focus,
:focus-visible {
  outline: 1px solid $blue;
}
body {
  @extend %df_cc;
  padding: 2em 0;
  font-size: 18px;
  font-weight: 400;
  line-height: 1.2;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: "Source Serif 4", sans-serif;
  color: $text;
  background-color: $bg;
}
input,
button,
textarea,
select {
  font: inherit;
}
p,
h1,
h2 {
  overflow-wrap: break-word;
}
#app {
  @extend %df_cc;
  flex-direction: column;
  padding: 0.5em 1em;
  box-shadow: 0px 10px 24px #adadad;
  border: 0.2em solid $accent;
  border-radius: 1em;
  isolation: isolate;
  min-height: 90vh;
}
.form {
  @extend %df_cc;
  flex-direction: column;
  row-gap: 1em;
  margin-top: 1em;
}
.info,
.service {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
</style>
