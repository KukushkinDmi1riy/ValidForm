
<template>
  <div id="#app">
    <div class="container">
      <form class="pt-4">
        <div class="form-group">
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            class='form-control'
            :class="{'is-invalid': $v.email.$error}"
            @change="$v.email.$touch()"
            v-model="email">
            <div class="invalid-feedback" v-if="!$v.email.required">
              Email filed is required
            </div>
            <div class="invalid-feedback" v-if="!$v.email.email">
              There should be an Email with @
            </div>
        </div>
        <div class="form-group">
          <label for="password">Password</label>
          <input
            type="password"
            id="password"
            class='form-control'
            :class="{'is-invalid': $v.$error}"
            @change="$v.password.$touch()"
            v-model="password">
            <div class="invalid-feedback" v-if="!$v.password.minLength">
              Too short password. Enter more then {{$v.password.$params.minLength.min}} values. Now is  {{this.password.length}}
            </div>

        </div>
        <div class="form-group">
          <label for="confirm">Confirm Password</label>
          <input
            type="password"
            id="confirm"
            class='form-control'
            :class="{'is-invalid': $v.$error}"
            @change="$v.confirmPassword.$touch()"
            v-model="confirmPassword">
            <div class="invalid-feedback" v-if="!$v.confirmPassword.sameAs">
                Passwords should math
            </div>
        </div>
        <pre> {{$v.email}}</pre>
        <hr>
        <pre> {{$v.password}}</pre>
      </form>
    </div>
  </div>
</template>

<script>

import { required , email, minLength, sameAs} from 'vuelidate/lib/validators'

export default {
 data: () => ({
    email: '',
    password: '',
    confirmPassword: '',
  }),
  validations: {
    email: {
      required,
      email
    },
    password: {
      minLength: minLength(6),
      required
    },
    confirmPassword: {
      sameAs: sameAs('password')
    }
  },
 };
</script>


<style>

</style>
