<template>
  <b-container class="">
    <b-row class="mx-auto">
      <h1>Your account information</h1>
      <div class="w-100"></div>
      <p class="text-gray-700">Manage your account info in this section.</p>
    </b-row>
    <b-container class="form--container px-5 py-5 bg-white border border-grey-500 rounded">
      <!-- Container Header -->
      <b-row align-h="between" class=" pb-4 border-bottom">
        <h2 class="text-gray-700">Your account information</h2>
        <b-button class="primaryBtn">Delete account</b-button>
        <div class="w-100 bg-gray-500" style="height: 1px"></div>
      </b-row>
      <!-- Container Body -->
      <b-row class="mt-2">
        <b-form class="account-info-form" inline style="">

          <!-- Main Fields -->
          <b-form-row id="main-fields">
            <div class="my-2">
              <label class="w-100 mb-1" for="inline-form-input-fname">First name</label>
              <b-form-input disabled id="inline-form-input-fname" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                placeholder="Victor">
              </b-form-input>
            </div>

            <div class="my-2">
              <label class="mb-1" for="inline-form-input-company">Company name <span>(Optional)</span></label>
              <b-form-input disabled id="inline-form-input-company" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                placeholder="Enter company name">
              </b-form-input>
            </div>

            <div class="pr-5 my-2">
              <label class="mb-1" for="inline-form-input-streetno">Street no.</label>
              <b-form-input id="inline-form-input-streetno" class="w-100 mb-2 mr-sm-2 mb-sm-0" placeholder="Street no">
              </b-form-input>
            </div>

            <div class="pr-5 my-2">
              <label class="mb-1" for="inline-form-input-name">Town / City</label>
              <b-form-input id="inline-form-input-town" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                placeholder="Enter town or city">
              </b-form-input>
            </div>

            <div class="pr-5 my-2">
              <label class="mb-1" for="inline-form-input-lname">Last name</label>
              <b-form-input id="inline-form-input-lname" class="w-100 mb-2 mr-sm-2 mb-sm-0" placeholder="Alex">
              </b-form-input>
            </div>

            <div class="pr-5 my-2">
              <label class="mb-1" for="inline-form-input-street">Street name</label>
              <b-form-input id="inline-form-input-street" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                placeholder="Enter street name">
              </b-form-input>
            </div>

            <div class="pr-5 my-2">
              <label class="mb-1" for="inline-form-input-postalcode">Postal code</label>
              <b-form-input id="inline-form-input-postalcode" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                placeholder="Enter postal code"></b-form-input>
            </div>

            <div class="my-2">
              <label class="mb-1 mr-sm-2" for="inline-form-custom-select-province">Province</label>
              <b-form-select id="inline-form-custom-select-province" class="w-100 mb-2 mr-sm-2 mb-sm-0"
                :options="[{ text: 'Choose...', value: null }, 'One', 'Two', 'Three']" :value="null"></b-form-select>
            </div>
          </b-form-row>

          <!-- Collapsible Fields -->
          <b-form-row class="w-100">
            <b-container cols class="collapsible-container">

              <b-row align-h="between" align-v="center" class="">
                <h2 class="m-0">Aditional Details</h2>
                <b-button v-b-toggle="'collapse'" class="m-1">Toggle Collapse</b-button>
              </b-row>

              <b-row>
                <b-collapse id="collapse" class="d-inline-flex">
                  <div class="pr-5 my-2">
                    <label class="mb-1" for="inline-form-input-AptNo">Do you have an Apt. Number?</label>
                    <b-form-input id="inline-form-input-AptNo" class=" mb-2 mr-sm-2 mb-sm-0"
                      placeholder="Apartment no."></b-form-input>
                  </div>

                  <div class="pr-5 my-2">
                    <label class="mb-1" for="inline-form-input-UnitNo">Do you have a Unit Number?</label>
                    <b-form-input id="inline-form-input-UnitNo" class=" mb-2 mr-sm-2 mb-sm-0"
                      placeholder="Unit no."></b-form-input>
                  </div>

                  <div class="pr-5 my-2">
                    <label class="mb-1" for="inline-form-input-AptNo">Do you have a PO Box Number?</label>
                    <b-form-input id="inline-form-input-AptNo" class=" mb-2 mr-sm-2 mb-sm-0"
                      placeholder="PO BOX"></b-form-input>
                  </div>
                </b-collapse>
              </b-row>

            </b-container>
          </b-form-row>

          <!-- Form Save Button -->
          <b-form-row class="w-100">
            Save
          </b-form-row>
        </b-form>
      </b-row>

    </b-container>

  </b-container>
</template>

<script>
export default {
  name: 'AccountInfo',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
// .form--container {
//   border: 1px solid slategray;
// }

$neutral-50: #F8FAFC;
$neutral-200: #E2E8F0;
$neutral-300: rgba(203, 213, 225, 1);
$neutral-500: #64748B;
$neutral-700: #334155;
$warning-300: #FEC84B;
$warning-25: #FFFCF5;

h1 {
  font-size: 24px;
  font-weight: 500;
}

h2 {
  font-size: 18px;
}

.primaryBtn {
  background-color: white;
  border: 1px solid $neutral-300;
  color: $neutral-700;

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
  }

  &[disabled] {
    color: $neutral-300;
  }
}

.account-info-form {
  min-width: 100%;

  #main-fields div {
    min-width: calc(50% - 30px);
  }

  #main-fields div:nth-child(2n) {
    margin-left: 30px;
  }

  label {
    font-size: 14px;
    font-weight: 500;
    justify-content: start;
    color: $neutral-700;
  }

  input {
    color: $neutral-500;
    border: 1px solid $neutral-300;
    border-radius: 0.5em;

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
</style>
