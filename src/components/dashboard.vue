<template>
  <section class="dashboard">
    <navbar></navbar>
    <!-- <b-container class="bv-example-row"> -->
      <b-row>
        <b-col>
          <information :population="population" :households="households" :district="district" :country="country" :locality="locality" :city="city" :status="status"></information>
        </b-col>
        <b-col>
          <b-card title="Card Title" tag="article" class="m-2">
            <!-- <expenditure></expenditure> -->
          </b-card>
        </b-col>
        <div class="w-100"></div>
        <b-col>
          <b-card v-if="locality&&monthlyincome" title="Demographics" :sub-title="'Monthly Income Distribution: '+locality" tag="article" class="m-2">
            <demographics :income="monthlyincome" :locality="locality"></demographics>
          </b-card>
          <b-card v-else title="Demographics" :sub-title="'Monthly Income Distribution: '+locality" tag="article" class="m-2">
            <span>No Data Found</span>
          </b-card>
        </b-col>
        <b-col>
          <b-card title="Expenditure" tag="article" class="m-2">
            <expenditure></expenditure>
          </b-card>
        </b-col>
      </b-row>
    <!-- </b-container> -->
  </section>
</template>
<script>
import navbar from './navbar'
import expenditure from './expenditure'
import demographics from './demographics'
import information from './information'
import pincode from '../assets/pincode.json'
import locality from '../assets/locality.json'
import income from '../assets/income.json'
export default {
  name: 'dashboard',
  components: {
    navbar,
    expenditure,
    demographics,
    information
  },
  props: [],
  data () {
    return {
      pincodejson: pincode,
      localityjson: locality,
      incomejson: income,
      monthlyincome: null,
      population: null,
      households: null,
      district: null,
      country: null,
      locality: null,
      city: null,
      status: null
    }
  },
  mounted () {
  },
  methods: {
    ShowOnPincode (num, status) {
      this.status = status
      this.population = null
      this.households = null
      this.district = null
      this.country = null
      this.locality = null
      this.city = null
      this.monthlyincome = null
      if (status === 'pincode') {
        if (this.pincodejson) {
          let features = this.pincodejson.features
          if (features.length > 0) {
            let attributes = features.filter((item) => {
              if (parseInt(item.attributes.pincode) === parseInt(num)) {
                return item.attributes
              }
            })
            if (attributes.length > 0) {
              this.population = attributes[0].attributes.population
              this.households = attributes[0].attributes.households
              this.district = attributes[0].attributes.district_n
              this.country = attributes[0].attributes.country
            }
          }
        }
      }
      if (status === 'locality') {
        if (this.localityjson) {
          let features = this.localityjson.features
          if (features.length > 0) {
            let attributes = features.filter((item) => {
              if (parseInt(item.attributes.locality_i) === parseInt(num)) {
                return item.attributes
              }
            })
            if (attributes.length > 0) {
              this.population = attributes[0].attributes.population
              this.households = attributes[0].attributes.households
              this.district = attributes[0].attributes.district_n
              this.country = attributes[0].attributes.country
              this.locality = attributes[0].attributes.locality
              this.city = attributes[0].attributes.city
            }
            if (this.locality) {
              let incomedata = this.incomejson.filter((item) => item.locality === this.locality)
              if (incomedata.length > 0) {
                this.monthlyincome = incomedata[0].income
              }
            }
          }
        }
      }
    }
  }
}

</script>
<style></style>
