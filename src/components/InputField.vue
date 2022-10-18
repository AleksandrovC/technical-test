<template>
  <div class="my-2 col-12 col-md-6" :class="(index % 2 == 0 ? 'pr-md-3' : 'pl-md-3')">

    <label class="w-100 mb-1" :for="field.id">
      {{ field.label }}
      <span v-if="field.isOptional && field.isShowOptional" class="optional"> (Optional)</span>
    </label>

    <div class="position-relative" :class="{ 'mr-lg-5': field.isShort }">
      <b-form-input
        :disabled="field.isDisabled"
        :id="field.id"
        :placeholder="field.placeholder"
        :value="field.value"
        :state="field.validationState"
        @input="$emit('inputChanged', {value: $event, currentField: field})"
        @keyup="field.isValidable && validateChars($event, field)"
        class="w-100 mb-2 mr-sm-2 mb-sm-0">
      </b-form-input>
      <b-form-invalid-feedback id="field.id" class="invalid-feedback">
      {{ field.placeholder }} can contain only numbers, letters, "/" and "-".
    </b-form-invalid-feedback>

      <div v-if="field.isPillable && field.value != ''" class="pill-container position-absolute h-100 d-flex">
        <div class="pill-input rounded-pill m-0 px-2 d-flex align-items-center">
          {{ field.value }}
          <span @click="$emit('closePill')" class="pl-1">x</span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import { bus } from '../main.js'

export default {
  name: 'InputField',
  props: {
    index: {
      type: Number,
      default: 0
    },
    field: {
      type: Object
    }
  },
  data () {
    return {
    }
  },
  methods: {

    validateChars: function ($event, field) {
      const message = { value: $event.target.value, currentField: field }
      bus.$emit('checkValidation', message)
    }
  }

}
</script>

<style lang="scss" scoped>
@import "../scss/input.scss";

.pill-container {
  top: 0;
  left: 0;
  padding: 0.375em 0.75em;

  .pill-input {
    font-size: 14px;
    background-color: $neutral-300;

    span {
      cursor: pointer;
    }
  }
}
</style>
