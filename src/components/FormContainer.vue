<template>
    <div>
        <b-row class="form-container px-3 px-md-5 py-5 mx-0 bg-white border border-grey-500">
            <!-- Container Header -->
            <b-row align-h="between" class="w-100 mx-0 pb-4 border-bottom">
                <h2 class="text-gray-700">Your account information</h2>
                <b-button class="primaryBtn d-none d-md-inline">Delete account</b-button>
                <div class="h-line w-100 bg-gray-500"></div>
            </b-row>
            <!-- Container Body -->
            <b-row class="mt-2 mx-0 w-100">
                <b-form class="account-info-form" inline>
                    <b-form-row id="main-fields" class="mx-0 mt-4 mb-3  w-100">

                        <!-- Main Input Fields -->

                        <InputField v-for="(field, index) in fields.mainFields" :key="field.id" :index="index"
                            v-bind:field="field" @inputChanged="updateInputValue($event)"
                            @closePill="deleteInputValue(field)">
                        </InputField>

                        <!-- Select Field -->

                        <SelectField v-bind:selectFields="selectFields" @selectChanged="updateSelect($event)">
                        </SelectField>

                    </b-form-row>

                    <!-- Collapsible -->

                    <CollapsibleCard v-bind:fields="fields" @inputChanged="updateInputValue($event, field)"
                        @checkValidation="validateCharacters($event)"></CollapsibleCard>

                </b-form>
            </b-row>

        </b-row>
        <b-row
            class="form-footer mx-0 flex-column flex-md-row px-3 px-md-5 py-3 py-md-5 bg-white border border-top-0 border-grey-500">
            <!-- Form Save Button -->
            <b-form-row class="">
                <b-button @click.prevent="submitForm()" :disabled="!allowSaveButton" class="primaryBtn w-100">Save
                    changes
                </b-button>
            </b-form-row>
        </b-row>
    </div>
</template>

<script>
import InputField from '../components/InputField.vue'
import SelectField from '../components/SelectField.vue'
import CollapsibleCard from '../components/CollapsibleCard.vue'
import { bus } from '../main.js'

export default {
  name: 'FormContainer',
  components: { InputField, SelectField, CollapsibleCard },
  data () {
    return {
      collapsibleOpen: false,
      fields: {
        mainFields: [

          {
            label: 'First name',
            placeholder: 'Victor',
            type: 'text',
            id: 'fName',
            isDisabled: true,
            isShort: false,
            isOptional: false,
            isShowOptional: false,
            isValidable: false,
            isPillable: false,
            value: 'Victor'
          },

          {
            label: 'Last name',
            placeholder: 'Alex',
            type: 'text',
            id: 'lName',
            isDisabled: true,
            isShort: false,
            isOptional: false,
            isShowOptional: false,
            isValidable: false,
            isPillable: false,
            value: 'Alex'
          },
          {
            label: 'Company name',
            placeholder: 'Enter company name',
            type: 'text',
            id: 'companyName',
            isDisabled: false,
            isShort: true,
            isOptional: true,
            isShowOptional: true,
            isValidable: false,
            isPillable: false,
            value: ''
          },
          {
            label: 'Street name',
            placeholder: 'Enter street name',
            type: 'text',
            id: 'streetName',
            isDisabled: false,
            isShort: true,
            isOptional: false,
            isShowOptional: false,
            isValidable: false,
            isPillable: true,
            value: ''
          },
          {
            label: 'Street no.',
            placeholder: 'Street no.',
            type: 'text',
            id: 'streetNo',
            isDisabled: false,
            isShort: true,
            isOptional: false,
            isShowOptional: false,
            isValidable: false,
            isPillable: true,
            value: ''
          },
          {
            label: 'Postal code',
            placeholder: 'Enter postal code',
            type: 'text',
            id: 'postalCode',
            isDisabled: false,
            isShort: true,
            isOptional: false,
            isShowOptional: false,
            isValidable: false,
            isPillable: true,
            value: ''
          },
          {
            label: 'Town / City',
            placeholder: 'Enter town or city',
            type: 'text',
            id: 'town',
            isDisabled: false,
            isShort: true,
            isOptional: false,
            isShowOptional: false,
            isValidable: false,
            isPillable: true,
            value: ''
          }

        ],
        aditionalFields: [
          {
            label: 'Do you have a Apt. Number?',
            placeholder: 'Apartment no.',
            type: 'text',
            id: 'aptNo',
            isDisabled: false,
            isShort: false,
            isOptional: false,
            isShowOptional: false,
            isValidable: true,
            isPillable: false,
            validationState: '',
            value: ''
          },
          {
            label: 'Do you have a Unit Number?',
            placeholder: 'Unit no.',
            type: 'text',
            id: 'unitNo',
            isDisabled: false,
            isShort: false,
            isOptional: false,
            isShowOptional: false,
            isValidable: true,
            isPillable: false,
            validationState: '',
            value: ''
          },
          {
            label: 'Do you have a PO Box Number?',
            placeholder: 'PO BOX',
            type: 'text',
            id: 'poBoxNumber',
            isDisabled: false,
            isShort: false,
            isOptional: false,
            isShowOptional: false,
            isValidable: true,
            isPillable: false,
            validationState: '',
            value: ''
          }
        ]
      },
      selectFields: [
        {
          label: 'Province',
          id: 'selectProvince',
          options: [
            // { value: '', text: 'Select', attr: 'selected disabled hidden' }
            // full list added by getSelectOptions()
          ],
          value: ''
        }
      ]

    }
  },
  mounted () {
    this.getSelectOptions()
  },
  beforeCreate () {
    bus.$on('checkValidation', (data) => {
      this.validateCharacters(data)
    })
  },
  destroyed () {
    bus.$off()
  },
  computed: {
    allowSaveButton: function () {
      // check required main fields have value
      return this.fields.mainFields.every(
        field => field.isOptional || (true &&
                    field.value !== null &&
                    field.value !== undefined &&
                    field.value !== '')) &&

                // check additional fields validation
                this.fields.aditionalFields.every(
                  field => field.validationState !== false
                ) &&

                // check select has value
                (this.selectFields.every(
                  select => select.value !== null &&
                        select.value !== undefined &&
                        select.value !== ''))
    }
  },

  methods: {
    deleteInputValue: function (currentField) {
      currentField.value = ''
    },
    updateInputValue: function (e) {
      e.currentField.value = e.value
      //   console.log(event)
    },
    getSelectOptions: async function () {
      await this.axios
        .get('https://roloca.coldfuse.io/judete')
        .then(response => (
          (response.data).forEach((el, i) => {
            this.selectFields[0].options.push({ value: el.nume, text: el.nume })
          })
        ))
    },
    updateSelect: function (event) {
      this.selectFields[0].value = event
    },
    validateCharacters: function (e) {
      const regex = /^[a-zA-Z0-9\s\-/]+$/g

      if (!regex.test(e.value) && e.value !== '') {
        e.currentField.validationState = false
      } else {
        e.currentField.validationState = true
      }
    //   console.log(e.currentField.value)
    },
    submitForm: function () {
      alert('Form successfully submited🎉')
    }
  }
}
</script>

<style lang="scss" scoped>
.form-container {
    border-radius: 0.5em 0.5em 0 0;

    label {
        white-space: pre
    }

    .h-line {
        height: 1px;
    }
}

.account-info-form {
    min-width: 100%;
}

.form-footer {
    background-color: $neutral-200 !important;
    border-radius: 0 0 0.5em 0.5em
}
</style>
