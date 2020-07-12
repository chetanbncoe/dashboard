<template>
<div>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">Geospoc Dashboard <br>
      <code v-if="pincode&&!locality">Individual pincode report for {{pincode}}</code>
      <code v-else>Locality ID {{locality}}</code>
      </b-navbar-brand>
    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
      </b-navbar-nav>
      <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-form-input type="number" size="sm" class="mr-sm-2" v-model="pincode" placeholder="PINCODE"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit" @click.prevent="show('pincode')">Show</b-button>
          &nbsp;  &nbsp;
          <b-form-input type="number" size="sm" class="mr-sm-2" v-model="locality" placeholder="LOCALITY"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit" @click.prevent="show('locality')">Show</b-button>
        </b-nav-form>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>
<script>
export default {
  name: 'dashboard',
  components: {},
  props: [],
  data () {
    return {
      pincode: null,
      locality: null
    }
  },
  mounted () {
    this.pincode = 560040
    this.show('pincode')
  },
  methods: {
    show (status) {
      if (status === 'locality') {
        this.$parent.ShowOnPincode(this.locality, status)
        this.pincode = null
      }
      if (status === 'pincode') {
        this.$parent.ShowOnPincode(this.pincode, status)
        this.locality = null
      }
    }
  }
}

</script>
<style>
</style>
