<template>
  <q-page class="flex flex-center">
    <div class="column">
        <div class="col">
          <img alt="English buoy logo" src="~assets/english-buoy-logo.png" width="256" height="256">
        </div>
        <div class="col">
          <Oauth :oauths="oauths" />
        </div>
    </div>
  </q-page>
</template>

<style>
</style>

<script>

import Oauth from 'bz-q-lib/src/components/Oauth'
export default {
  components: {
    Oauth
  },
  data: function () {
    return {
      oauths: [
        {
          type: 'google',
          url: '/api/google'
        }
      ]
    }
  },
  name: 'PageIndex'
}
</script>
