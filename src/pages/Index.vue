<template>
  <q-page class="flex flex-center column q-pa-lg">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-full.svg"

    >
    <q-btn label="Check for update" @click="checkUpdate" style="margin-top: 20px" />
    <div class="column col" style="margin-top: 20px">
      <div class="col-auto">
        isUpdateAvailable: {{ isUpdateAvailable }}
      </div>
      <div class="col-auto">
        isUpdateDownloaded: {{ isUpdateDownloaded }}
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      isUpdateAvailable: false,
      isUpdateDownloaded: false,
    }
  },
  methods: {
    checkUpdate () {
      const { app, autoUpdater, dialog } = require('electron').remote

      const server = 'https://au-test-app.logicalmindapps.vercel.app'
      const url = `${server}/update/${process.platform}/${app.getVersion()}`

      console.log('url:')
      console.log(url)

      autoUpdater.setFeedURL({ url })

      autoUpdater.checkForUpdates()

      autoUpdater.on('update-downloaded', (event, releaseNotes, releaseName) => {
        console.log('UPDATE FOUND!')
      })

      autoUpdater.on('error', message => {
        console.error('There was a problem updating the application')
        console.error(message)
      })

    },
  }
}
</script>
