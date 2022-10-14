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
      <b-row class="form--container px-3 px-md-5 py-5 mx-0 bg-white border border-grey-500"
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
            <!-- Main Fields -->
            <b-form-row id="main-fields" class="mx-0 mt-4 mb-3  w-100">

              <div v-for="(field, index) in fields" :key="field.id" class="my-2 col-12 col-md-6"
                :class="{ 'pr-lg-5': field.isShort }">

                <label class="w-100 mb-1" :for="field.id">
                  {{ field.label }}
                  <span v-if="field.isOptional" class="optional"> (Optional)</span>
                </label>

                <div class="position-relative">
                  <b-form-input :disabled="field.isDisabled" :id="field.id" :placeholder="field.placeholder"
                    v-model="field.value" class="w-100 mb-2 mr-sm-2 mb-sm-0">
                  </b-form-input>
                  <div v-if="field.isPillable && field.value != ''"
                    class="pill-container position-absolute h-100 d-flex">
                    <div class="pill-input rounded-pill m-0 px-2 d-flex align-items-center">
                      {{ field.value }}
                      <span v-on:click="deleteValue(index)" class="pl-1">x</span>
                    </div>
                  </div>
                </div>

              </div>

              <!-- <div v-for="field in fields" :key="field.id" class="my-2 col-12 col-md-6"
                :class="{ 'pr-lg-5': field.isShort }">
                <label class="w-100 mb-1" :for="field.id">
                  {{ field.label }}
                  <span v-if="field.isOptional" class="optional"> (Optional)</span>
                </label>
                <b-form-input :disabled="field.isDisabled" :id="field.id" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                  :placeholder="field.placeholder">
                </b-form-input>
              </div> -->

              <div class="my-2 col-12 col-md-6">
                <label class="mb-1 mr-sm-2" for="inline-form-custom-select-province">Province</label>
                <div class="position-relative">
                  <b-form-select id="inline-form-custom-select-province" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                    :options="[{ text: 'Choose...', value: null }, 'One', 'Two', 'Three']" :value="null">
                    <div> test</div>
                  </b-form-select>
                  <b-icon class="select-custom-arrow position-absolute" icon="chevron-down"></b-icon>
                </div>
              </div>

            </b-form-row>

            <!-- Collapsible Fields -->
            <b-form-row class="w-100 mx-0">
              <b-container cols class="collapsible-container px-3">

                <b-row align-h="between" align-v="center" class="mx-0 py-3">
                  <h2 class="m-0">Aditional Details</h2>
                  <b-button v-b-toggle="'collapse'" class="primaryBtn m-0 px-2">
                    <b-icon icon="chevron-down"></b-icon>
                  </b-button>

                </b-row>

                <b-row class="mx-0 pr-lg-5 mr-lg-5">
                  <b-collapse id="collapse" class="w-100">
                    <section class="d-flex flex-wrap justify-content-between row">
                      <div class="my-2 col-12 col-md-6 col-lg-4">
                        <label class="mb-1" for="inline-form-input-AptNo">Do you have an Apt. Number?</label>
                        <b-form-input id="inline-form-input-AptNo" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                          placeholder="Apartment no."></b-form-input>
                      </div>

                      <div class="my-2 col-12 col-md-6 col-lg-4">
                        <label class="mb-1" for="inline-form-input-UnitNo">Do you have a Unit Number?</label>
                        <b-form-input id="inline-form-input-UnitNo" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                          placeholder="Unit no.">
                        </b-form-input>
                      </div>

                      <div class="my-2 col-12 col-md-6 col-lg-4">
                        <label class="mb-1" for="inline-form-input-AptNo">Do you have a PO Box Number?</label>
                        <b-form-input id="inline-form-input-AptNo" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                          placeholder="PO BOX">
                        </b-form-input>
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
          <b-button class="primaryBtn w-100">Save changes</b-button>
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
          value: ''
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
          value: ''
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

      ]
    }
  },
  methods: {
    deleteValue: function (e) {
      // this.message = this.message.split('').reverse().join('')
      this.fields[e].value = ''
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
  &:active {
    background-color: white !important;
    box-shadow: 0 0 0 0.2rem rgb(130 138 145 / 50%) !important;
    color: $neutral-700 !important;
    border: 1px solid $neutral-300 !important;
    // box-shadow: 0px 0px 0px 4px rgba(242, 244, 247, 1) !important;

    // box-shadow: 0px 1px 2px 0px rgba(16, 24, 40, 0.05) !important;

  }

  &[disabled] {
    color: $neutral-300;
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

  &:focus,
  &:active {
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
  &:active,
  &:focus {
    background-color: $warning-100 !important;
    color: $warning-700 !important;
  }
}

.form--container {
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

  input {
    color: $neutral-500;
    border: 1px solid $neutral-300;
    border-radius: 0.5em;

    &:focus {
      // box-shadow: 0px 0px 0px 4px rgb(249, 236, 224, 1) !important;

      // box-shadow: 0px 1px 2px 0px rgb(249, 243, 236, 1) !important;
      // box-shadow: 0 0 0 0.2rem $warning-100 !important;
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
  right: 0;
  height: calc(100% - 4px);
  margin-right: 0.5em;
  background: white;
  margin-top: 2px;
  margin-bottom: 2px;
  //  border-top: 1px solid $neutral-300;
  //  border-bottom: 1px solid $neutral-300;

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
  }
}

.form--footer {
  background-color: $neutral-200 !important;
}
</style>
