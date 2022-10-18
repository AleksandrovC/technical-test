<template>
  <b-container class="my-lg-5 my-md-4 my-3">
    <div class="px-3">
      <b-row class="page-header mx-auto" align-h="between">
        <b-col class="px-0">
          <h1>Account info</h1>
          <div class="w-100"></div>
          <p class="d-none d-md-block">Manage your account info in this section.</p>
        </b-col>
        <b-col class="px-0 pb-2 d-flex justify-content-end align-items-start">
          <b-button class="secondaryBtn  d-lg-none text-nowrap">
            <b-icon icon="arrow-left-short"></b-icon>Go back to previous page
          </b-button>
        </b-col>
      </b-row>

      <FormContainer></FormContainer>

      <div>
        <div class="mt-3 d-md-none text-center">
          <b-button class="ghostBtn">Delete account</b-button>
        </div>
      </div>
    </div>
  </b-container>
</template>

<script>

import FormContainer from '../components/FormContainer.vue'
export default {
  name: 'AcountInfo',
  components: { FormContainer }
}
</script>

<style scoped lang="scss">
.page-header {
  p {
    font-size: 14px
  }
}

</style>
