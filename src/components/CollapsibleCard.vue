<template>
    <b-form-row class="w-100 mx-0">
        <b-container cols class="collapsible-container px-3">

            <b-row align-h="between" align-v="center" class="mx-0 py-3">
                <h2 class="m-0">Aditional Details</h2>
                <b-button :class="collapsibleOpen ? null : 'collapsed'"
                    :aria-expanded="collapsibleOpen ? 'true' : 'false'" aria-controls="collapse-4"
                    @click="collapsibleOpen = !collapsibleOpen" class="primaryBtn m-0 px-2">
                    <b-icon icon="chevron-up" :class="collapsibleOpen ? null : 'rotate-180'"></b-icon>
                </b-button>

            </b-row>

            <b-row class="mx-0">
                <b-collapse v-model="collapsibleOpen" class="w-100 mt-n2 mb-2">
                    <section class="d-flex flex-wrap justify-content-between row">
                        <!-- Additional Fields -->

                        <InputField v-for="(field, index) in fields.aditionalFields" :key="field.id" :index="index"
                            v-bind:field="field" class="col-lg-4">
                        </InputField>

                    </section>
                </b-collapse>
            </b-row>

        </b-container>
    </b-form-row>
</template>

<script>
import InputField from '../components/InputField.vue'

export default {
  name: 'CollapsibleCard',
  components: { InputField },
  props: {
    fields: {
      type: Object
    }
  },
  data () {
    return {
      collapsibleOpen: false
    }
  }
}
</script>

<style lang="scss" scoped>
.collapsible-container {
  background-color: $warning-25;
  border: 1px solid $warning-300;
  border-radius: 12px;
}

</style>
