<template>
  <b-card class="m-2">

    <b-card-group>
      <b-card v-if="population" :title="population.toString()" sub-title="Population">
      </b-card>
      <b-card v-else title="No Data Found" sub-title="Population">
      </b-card>
      <b-card v-if="households" :title="households.toString()" sub-title="Households">
      </b-card>
      <b-card v-else title="No Data Found" sub-title="Households">
      </b-card>
    </b-card-group>

    <b-card-group v-if="status==='pincode'" class="mt-1">
      <b-card :title="district" sub-title="District">
      </b-card>
      <b-card :title="country" sub-title="Country">
      </b-card>
    </b-card-group>
    <b-card-group v-if="status==='locality'" class="mt-1">
          <b-card :title="locality" sub-title="Locality">
          </b-card>
          <b-card :title="city" sub-title="City">
          </b-card>
        </b-card-group>
  </b-card>
</template>
<script>
export default {
  name: 'dashboard',
  components: {
  },
  props: ['population', 'households', 'district', 'country', 'locality', 'city', 'status'],
  data () {
    return {
    }
  },
  mounted () {
  },
  methods: {

  }
}
</script>

<style>

</style>
