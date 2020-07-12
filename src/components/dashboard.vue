<template>
<section class="dashboard">
  <navbar></navbar>
  <b-container class="bv-example-row">
  <b-row>
    <b-col>
      <chart></chart>
    </b-col>
    <b-col>Column</b-col>
    <div class="w-100"></div>
    <b-col>Column</b-col>
    <b-col>Column</b-col>
  </b-row>
</b-container>
</section>
</template>
<script>
import navbar from './navbar'
import chart from './chart'
export default {
  name: 'dashboard',
  components: {navbar, chart},
  props: [],
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
<style></style>
