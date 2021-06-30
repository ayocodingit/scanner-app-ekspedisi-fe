<template>
  <div id="app">
    <navbar />
    <section id="app">
      <div class="container">
        <div class="row mt-2">
          <div class="col">
            <header-info />
          </div>
        </div>

        <div class="row">
          <div class="col-sm-4">
            <form-scan />
          </div>
          <div class="col-sm-8">
            <list-ekspedisi />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import FormScan from './components/FormScan.vue'
  import HeaderInfo from './components/HeaderInfo.vue'
  import ListEkspedisi from './components/ListEkspedisi.vue'
  import Navbar from './components/Navbar.vue'

  export default {
    name: 'App',
    components: {
      Navbar,
      ListEkspedisi,
      FormScan,
      HeaderInfo
    }
  }
</script>