<template>
  <section class="dashboard">
    <navbar></navbar>
    <!-- <b-container class="bv-example-row"> -->
      <b-row>
        <b-col>
          <information :population="population" :households="households" :district="district" :country="country" :locality="locality" :city="city" :status="status"></information>
        </b-col>
        <b-col v-if="mapdata.length>0" class="m-1">
            <position :mapdata="mapdata"></position>
        </b-col>
        <b-col v-else class="m-1 text-center">No Data Found</b-col>
        <div class="w-100"></div>
        <b-col>
          <b-card v-if="locality&&monthlyincome" title="Demographics" tag="article" class="m-2">
            <demographics :income="monthlyincome" :locality="locality"></demographics>
          </b-card>
          <b-card v-else title="Demographics" tag="article" class="m-2">
            <span>No Data Found</span>
          </b-card>
        </b-col>
        <b-col>
          <b-card v-if="expenditurearr.length>0" title="Expenditure" tag="article" class="m-2">
            <expenditure :expenditurearr="expenditurearr"></expenditure>
          </b-card>
          <b-card v-else title="Expenditure" tag="article" class="m-2">
            <span>No Data Found</span>
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
import position from './position'
import pincode from '../assets/pincode.json'
import locality from '../assets/locality.json'
import income from '../assets/income.json'
import expendituredata from '../assets/expenditure.json'

export default {
  name: 'dashboard',
  components: {
    navbar,
    expenditure,
    demographics,
    information,
    position
  },
  props: [],
  data () {
    return {
      expenditurejson: expendituredata,
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
      status: null,
      expenditurearr: [],
      expincode: null,
      mapdata: []
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
      this.expincode = null
      this.expenditurearr = []
      this.mapdata = []
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
            let geodata = features.filter((item) => {
              if (parseInt(item.attributes.pincode) === parseInt(num)) {
                return item.geometry
              }
            })
            if (geodata.length > 0) {
              this.mapdata = geodata[0].geometry.rings
            }
            if (attributes.length > 0) {
              this.population = attributes[0].attributes.population
              this.households = attributes[0].attributes.households
              this.district = attributes[0].attributes.district_n
              this.country = 'India'
            }
            if (num) {
              this.expenditurearr = this.expenditurejson.filter((item) => parseInt(item.pincode) === parseInt(num))
              if (this.expenditurearr.length > 0) {
                this.expincode = this.expenditurearr[0].pincode
              }
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
            let geodata = features.filter((item) => {
              if (parseInt(item.attributes.locality_i) === parseInt(num)) {
                return item.geometry
              }
            })
            if (geodata.length > 0) {
              this.mapdata = geodata[0].geometry.rings
            }
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
