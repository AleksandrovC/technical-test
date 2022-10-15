<template>
  <b-container class="my-lg-5 my-md-4 my-3">
    <div class="px-3">
      <b-row class="mx-auto" align-h="between">
        <b-col class="px-0">
          <h1>Account info</h1>
          <div class="w-100"></div>
          <p class="text-gray-700 d-none d-md-block">Manage your account info in this section.</p>
        </b-col>
        <b-col class="px-0 pb-2 d-flex justify-content-end align-items-start">
          <b-button class="secondaryBtn  d-lg-none text-nowrap">
            <b-icon icon="arrow-left-short"></b-icon>Go back to previous page
          </b-button>
        </b-col>
      </b-row>
      <b-row class="form-container px-3 px-md-5 py-5 mx-0 bg-white border border-grey-500"
        style="border-radius: 0.5em 0.5em 0 0">
        <!-- Container Header -->
        <b-row align-h="between" class="w-100 mx-0 pb-4 border-bottom">
          <h2 class="text-gray-700">Your account information</h2>
          <b-button class="primaryBtn d-none d-md-inline">Delete account</b-button>
          <div class="w-100 bg-gray-500" style="height: 1px"></div>
        </b-row>
        <!-- Container Body -->
        <b-row class="mt-2 mx-0 w-100">
          <b-form class="account-info-form" inline style="">
            <b-form-row id="main-fields" class="mx-0 mt-4 mb-3  w-100">
              <!-- Main Input Fields -->
              <div v-for="(field, index) in fields" :key="field.id" class="my-2 col-12 col-md-6"
                :class="(index % 2 == 0 ? 'pr-md-3' : 'pl-md-3')">

                <label class="w-100 mb-1" :for="field.id">
                  {{ field.label }}
                  <span v-if="field.isOptional" class="optional"> (Optional)</span>
                </label>

                <div class="position-relative" :class="{ 'mr-lg-5': field.isShort }">
                  <b-form-input :disabled="field.isDisabled" :id="field.id" :placeholder="field.placeholder"
                    v-model="field.value" class="w-100 mb-2 mr-sm-2 mb-sm-0">
                  </b-form-input>
                  <div v-if="field.isPillable && field.value != ''"
                    class="pill-container position-absolute h-100 d-flex">
                    <div class="pill-input rounded-pill m-0 px-2 d-flex align-items-center">
                      {{ field.value }}
                      <span v-on:click="deleteInputValue(index)" class="pl-1">x</span>
                    </div>
                  </div>
                </div>

              </div>

              <!-- Select Field -->

              <div class="my-2 col-12 col-md-6 pl-md-3 mb-2">
                <label class="mb-1 mr-sm-2" for="selectProvince">Province</label>
                <div class="position-relative">
                  <b-form-select id="selectProvince" class="w-100 mr-sm-2 mb-sm-0"
                    :options="selectFields[0].options" :value="null">
                    <div> test</div>
                  </b-form-select>
                  <b-icon class="select-custom-arrow position-absolute" icon="chevron-down"></b-icon>
                </div>
              </div>

            </b-form-row>

            <!-- Collapsible -->
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

                <b-row class="mx-0 pr-lg-5 mr-lg-5">
                  <b-collapse v-model="collapsibleOpen" class="w-100">
                    <section class="d-flex flex-wrap justify-content-between row">
                      <!-- Additional Fields -->
                      <div v-for="(aditionalField, index) in aditionalFields" :key="aditionalField.id"
                        class="my-2 col-12 col-md-6 col-lg-4">
                        <label class="" :for="aditionalField.id">Do you have a {{ aditionalField.label }}</label>
                        <b-form-input v-model="aditionalField.value" :id="aditionalField.id"
                          :state="aditionalField.validationState" class="w-100 mt-1 mb-2 mr-sm-2"
                          :placeholder="aditionalField.placeholder" @keyup="validateState(index)"></b-form-input>
                        <b-form-invalid-feedback id="aditionalField.id">
                          {{ aditionalField.label }} can contain only numbers, letters, "/" and "-".
                        </b-form-invalid-feedback>
                      </div>

                    </section>
                  </b-collapse>
                </b-row>

              </b-container>
            </b-form-row>

          </b-form>
        </b-row>

      </b-row>
      <b-row
        class="form--footer mx-0 flex-column flex-md-row px-3 px-md-5 py-3 py-md-5 bg-white border border-top-0 border-grey-500"
        style="border-radius: 0 0 0.5em 0.5em">
        <!-- Form Save Button -->
        <b-form-row class="">
          <b-button @click.prevent="submitForm()" :disabled="!allowSaveButton" class="primaryBtn w-100">Save changes
          </b-button>
        </b-form-row>
      </b-row>
      <div>
        <div class="mt-3 d-md-none text-center">
          <b-button class="ghostBtn">Delete account</b-button>
        </div>
      </div>
    </div>
  </b-container>
</template>

<script>
export default {
  name: 'AccountInfo2',
  props: {
    msg: String
  },
  data () {
    return {
      collapsibleOpen: false,
      fields: [

        {
          label: 'First name',
          placeholder: 'Victor',
          type: 'text',
          id: 'fName',
          isDisabled: true,
          isShort: false,
          isOptional: false,
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
          isPillable: true,
          value: ''
        }

      ],
      selectFields: [
        {
          label: 'Province',
          id: 'selectProvince',
          options: [
            { value: null, text: 'Select' }
            // full list added by getSelectOptions()
          ]
        }
      ],
      aditionalFields: [
        {
          label: 'Apt. Number',
          placeholder: 'Apartment no.',
          type: 'text',
          id: 'aptNo',
          isDisabled: false,
          isShort: false,
          isOptional: false,
          isPillable: false,
          validationState: '',
          value: ''
        },
        {
          label: 'Unit Number',
          placeholder: 'Unit no.',
          type: 'text',
          id: 'unitNo',
          isDisabled: false,
          isShort: false,
          isOptional: false,
          isPillable: false,
          validationState: '',
          value: ''
        },
        {
          label: 'PO Box Number',
          placeholder: 'PO BOX',
          type: 'text',
          id: 'poBoxNumber',
          isDisabled: false,
          isShort: false,
          isOptional: false,
          isPillable: false,
          validationState: '',
          value: ''
        }
      ],
      errors: []
    }
  },
  mounted () {
    this.getSelectOptions()
  },
  computed: {
    allowSaveButton: function () {
      return this.fields.every(
        field => field.value !== null &&
          field.value !== undefined &&
          field.value !== '') &&
        this.aditionalFields.every(
          aditionalField => aditionalField.validationState !== false
        )
    }
  },

  methods: {
    validateState: function (i) {
      const inputValue = this.aditionalFields[i].value
      const regex = /^[a-zA-Z0-9\s\-/]+$/g

      if (!regex.test(inputValue) && inputValue !== '') {
        this.aditionalFields[i].validationState = false
      } else {
        this.aditionalFields[i].validationState = true
      }
    },
    deleteInputValue: function (e) {
      this.fields[e].value = ''
    },
    submitForm () {
      alert('Form successfully submitted🎉')
    },
    getSelectOptions: async function () {
      await this.axios
        .get('https://roloca.coldfuse.io/judete')
        .then(response => (
          (response.data).forEach((el, i) => {
            this.selectFields[0].options.push({ value: el.nume, text: el.nume })
          })
        ))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$neutral-50: #F8FAFC;
$neutral-200: #E2E8F0;
$neutral-300: #cbd5e1;
$neutral-400: #a2abb8;
$neutral-500: #6e7886;
$neutral-700: #334155;
$netural-900: #052843;
$warning-25: #FFFCF5;
$warning-50: #F9F3EC;
$warning-100: #f9ece0;
$warning-300: #FEC84B;
$warning-700: #F9A24B;
$warning-800: #F99632;

h1 {
  font-size: 24px;
  font-weight: 500;
}

h2 {
  font-size: 18px;
  color: $netural-900;
}

.rotate-180 {
  transform: rotate(180deg);
}

.primaryBtn {
  background-color: white;
  border: 1px solid $neutral-300;
  color: $neutral-700;
  border-radius: 0.5em;

  &:hover {
    background-color: $neutral-50;
    border: 1px solid $neutral-300;
    color: $neutral-700;
  }

  &:focus,
  &:enabled:active {
    background-color: white !important;
    // box-shadow: 0 0 0 0.2rem rgb(130 138 145 / 50%) !important;
    box-shadow: 0px 0px 0px 4px rgba(242, 244, 247, 1);
    box-shadow: 0px 1px 2px 0px rgba(16, 24, 40, 0.01);

    color: $neutral-700 !important;
    border: 1px solid $neutral-300 !important;
  }

  &[disabled] {
    color: $neutral-300;
    background-color: white;
    border-color: $neutral-200 !important;
  }
}

.secondaryBtn {
  background-color: $warning-50;
  border: 1px solid $warning-50;
  color: $warning-800;
  border-radius: 0.5em;
  font-size: 14px;

  &:hover {
    background-color: $warning-100;
    border: 1px solid $warning-100;
    color: $warning-700;
  }

  &:focus{
    background-color: $warning-50 !important;
    border: 1px solid $warning-50 !important;
    box-shadow: 0 0 0 0.2rem $warning-100 !important;
    color: $warning-700 !important;
  }
  &:enabled:active {
    background-color: $warning-50 !important;
    border: 1px solid $warning-50 !important;
    box-shadow: 0 0 0 0.2rem $warning-100 !important;
    color: $warning-700 !important;
  }

  &[disabled] {
    background-color: $warning-25;
    color: $warning-300;
  }
}

.ghostBtn {
  color: $warning-700;
  background-color: transparent;
  border: none;

  &:hover,
  &:enabled:active {
    background-color: $warning-100 !important;
    color: $warning-700 !important;
    box-shadow: 0 0 0 0.2rem $warning-100 !important;
  }
  &:focus {
    background-color: transparent;
    color: $warning-700 !important;
    box-shadow: none;

  }

  //     color: #fff;
    // background-color: #5a6268;
    // border-color: #545b62;
    // box-shadow: 0 0 0 0.2rem rgb(130 138 145 / 50%);
}

.form-container {
  border-radius: 0.5em 0.5em 0 0;

  label {
    white-space: pre
  }
}

.account-info-form {
  min-width: 100%;

  // #main-fields div {
  //   // min-width: calc(50% - 15px);
  // }

  label {
    font-size: 14px;
    font-weight: 500;
    justify-content: start;
    color: $neutral-700;
    white-space: pre;
  }

  label .optional {
    color: $neutral-400;
  }

  input, select {
    color: $neutral-500;
    border: 1px solid $neutral-300;
    border-radius: 0.5em;

    &:focus {
      border: 1px solid $warning-300;
      box-shadow: 0px 0px 0px 4px $warning-100 !important;
      box-shadow: 0px 1px 2px 0px rgba(249, 243, 236, 1);

    }

    &:disabled {
      background-color: $neutral-50 !important;
    }
  }

}

.collapsible-container {
  background-color: $warning-25;
  border: 1px solid $warning-300;
  border-radius: 12px;
}
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

.pill-container {
  top: 0;
  left: 0;
  padding: 0.375em 0.75em;

  .pill-input {
    // position: absolute;
    // top:0;
    // left:0;
    font-size: 14px;
    background-color: $neutral-300;

    span {
      cursor: pointer;
    }
  }
}

.form--footer {
  background-color: $neutral-200 !important;
}

.is-valid {
  border-color: green;
  background-image: none !important;
}

.is-invalid {
  border-color: red !important;
  background-image: none !important;

}
</style>
