<template>
  <div class="my-2 col-12 col-md-6 pl-md-3 mb-2">
                <label class="mb-1 mr-sm-2" for="selectProvince">Province</label>
                <div class="position-relative">
                  <b-form-select id="selectProvince"
                  class="w-100 mr-sm-2 mb-sm-0"
                  :value="selectFields[0].value"
                  :attr="selectFields[0].attr"
                  @change="$emit('selectChanged', $event)">
                  <option value="" selected disabled hidden>Select</option>
                  <option v-for="option in selectFields[0].options" :value=option.value :key="option.value">{{ option.value }}</option>

                  </b-form-select>
                  <b-icon class="select-custom-arrow position-absolute" icon="chevron-down"></b-icon>
                </div>
              </div>
</template>

<script>
export default {
  name: 'SelectField',
  props: {
    index: {
      type: Number,
      default: 0
    },
    selectFields: {
      type: Array
    }
  },
  data () {
    return {
    }
  }

}
</script>

<style lang="scss" scoped>
 @import "../scss/input.scss";
.select-custom-arrow {
  pointer-events: none;
  position: absolute;
  top: 0;
  right: 2px;
  height: calc(100% - 4px);
  margin-right: 0.5em;
  background: white;
  margin-top: 2px;
  margin-bottom: 2px;
}

</style>
