<template>
<div class="hello">
  <h1>{{ msg }}</h1>
  <div>
    <div class="form-group" v-bind:class="{ 'form-group--error': $v.person.name.$error }">
      <label class="form__label" for="uname">name</label>
      <input class="form__input" id="uname" v-model.trim="person.name" @input="$v.person.name.$touch()">
    </div>
    <span class="form-group__message" v-if="!$v.person.name.required">Field is required</span>
    <span class="form-group__message" v-if="!$v.person.name.minLength">
      Name must have at least {{$v.person.name.$params.minLength.min}} letters.
    </span>
    <br>
    <br>
    <div class="form-group" v-bind:class="{ 'form-group--error': $v.person.age.$error }">
      <label class="form__label" for="age">age</label>
      <input class="form__input" id="age" v-model.trim="person.age" @blur="$v.person.age.$touch()">
    </div>
    <span class="form-group__message" v-if="!$v.person.age.between">
      Must be between {{$v.person.age.$params.between.min}} and {{$v.person.age.$params.between.max}}
    </span>
    <br>
    <span class="form-group__message" v-if="!$v.person.age.numeric"> Must be a number</span>
    <br>
    <br>
    <span class="form_val" v-if="!$v.person.$invalid">Person's name or age inputting is validate.</span>
    <br>
    <!-- <span v-if="!$v.person.age.range">哇！18岁的花季童鞋耶</span> -->
    <pre> {{$v}}</pre>
  </div>

</div>
</template>

<script>
import { required, minLength, between, numeric } from 'vuelidate/lib/validators'
export default {
  name: 'hello',
  data() {
    return {
      msg: 'Study Vuelidator',
      person: {
        name: '',
        age: 0,
      }

    }
  },
  validations: {
    person: {
      name: {
        required,
        minLength: minLength(4),
      },
      age: {
        between: between(10,30),
        numeric,
        // range (val) {
        //   if(val == 18) {
        //     return true
        //   }
        // }
      }
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-group--error,
.form-group__message{
  color:red;
}
.form_val {
  color: blue;
}
</style>
