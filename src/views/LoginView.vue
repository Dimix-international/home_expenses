<template>
  <form class="card auth-card" @submit.prevent="submitHandler">
    <div class="card-content">
      <span class="card-title">Домашняя бухгалтерия</span>
      <div class="input-field">
        <input
            id="email"
            type="text"
            v-model.trim="email"
            :class="{invalid: ($v.email.$dirty && !$v.email.required) || ($v.email.$dirty && !$v.email.email)}"
        >
        <label for="email">Email</label>
        <small
            v-if="$v.email.$dirty && !$v.email.required"
            class="helper-text invalid"
        >
          Empty email field
        </small>
        <small
            v-else-if="$v.email.$dirty && !$v.email.e"
            class="helper-text invalid"

        >
          Incorrect email!
        </small>
      </div>
      <div class="input-field">
        <div>Пароль</div>
        <input
            id="password"
            v-model.trim="password"
            :class="{invalid: ($v.email.$dirty && !$v.password.required)
            || ($v.email.$dirty && !$v.password.minLength)}"
        >
        <small
            v-if="$v.password.$dirty && !$v.password.required"
            class="helper-text invalid"
        >
          Empty password field
        </small>
        <small
            v-else-if="$v.password.$dirty && !$v.password.minLength"
            class="helper-text invalid"
        >
          Incorrect password! Min {{$v.password.$params.minLength.min}}
        </small>
      </div>
    </div>
    <div class="card-action">
      <div>
        <button
            class="btn waves-effect waves-light auth-submit"
            type="submit"
        >
          Войти
          <i class="material-icons right">send</i>
        </button>
      </div>

      <p class="center">
        Нет аккаунта?
        <router-link to="/register">Зарегистрироваться</router-link>
      </p>
    </div>
  </form>
</template>

<script>
import {email, required, minLength} from 'vuelidate/lib/validators';

export default {
  name: "LoginView",
  data: () => ({
    email: '',
    password: '',
  }),
  validations: {
    email: {email, required},
    password: {required, minLength: minLength(6)}
  },
  methods: {
    submitHandler() {
      //$v - системная переменная из либы vuelidate
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }

      const formData = {
        email: this.email,
        password: this.password
      }

      console.log('formData', formData);

      this.$router.push('/');
    }
  }
}
</script>

<style scoped>

</style>