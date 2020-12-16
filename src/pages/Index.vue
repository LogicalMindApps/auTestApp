<template>
  <q-page class="flex flex-center column q-pa-lg">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-full.svg"

    >
    <div class="column col" style="padding-top: 20px">
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
  created () {
    const { ipcRenderer } = require('electron')
    ipcRenderer.on('update_available', () => {
      ipcRenderer.removeAllListeners('update_available')
    })
    ipcRenderer.on('update_downloaded', () => {
      ipcRenderer.removeAllListeners('update_downloaded')
    })
  }

}
</script>
