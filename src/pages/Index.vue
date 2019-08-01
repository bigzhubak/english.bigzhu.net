<template>
  <q-page padding class="">
    <div class="column">
        <div class="col">
          <img alt="English buoy logo" src="~assets/english-buoy-logo.png" width="144" height="144">
        </div>
        <div class="col">
          <Oauth :oauths="oauths" />
        </div>
    </div>
    <form @submit.prevent="simulateSubmit" class="q-pa-md">
      <q-input
        filled
        color="teal"
        hint="youtube url"
        v-model="youtube"
      />
      <!-- a simple text field watching for the enter key release -->
      <q-input
        type="textarea"
        filled
        color="teal"
        hint="Type then hit Enter key above"
        v-model="article"
      />

      <!--
        A button with v-model set to submit.
        v-model scope variable must be a strict Boolean
      -->
      <div class="row justify-end">
        <q-btn
          type="submit"
          :loading="submitting"
          label="Save"
          class="q-mt-md"
          color="teal"
        >
          <template v-slot:loading>
            <q-spinner-facebook />
          </template>
        </q-btn>
      </div>
    </form>
  </q-page>
</template>

<style>
</style>

<script>
import axios from 'axios'
import Oauth from 'bz-q-lib/src/components/Oauth'
export default {
  components: {
    Oauth
  },
  data: function () {
    return {
      youtube: '',
      article: '',
      submitting: false,
      oauths: [
        {
          type: 'google',
          url: '/api/google'
        }
      ]
    }
  },
  methods: {
    simulateSubmit () {
      this.submitting = true
      axios.post('/api/Subtitle', { article: this.article, Youtube: this.youtube }).then(() => {
        this.submitting = false
        this.article = ''
        this.youtube = ''
      }).catch((error) => {
        this.$q.notify(error.response.data)
        this.submitting = false
      })
      // Simulating a delay here.
      // When we are done, we reset "submitting"
      // Boolean to false to restore the
      // initial state.
    }
  },
  name: 'PageIndex'
}
</script>
