<template>
  <div class="agora-demo">
    <button @click="join">Join Channel</button>
    <div ref="remoteContainer"></div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import AgoraRTC from 'agora-rtc-sdk-ng'

const appId = 'YOUR_AGORA_APP_ID'
const token = null
const channel = 'test'

const client = AgoraRTC.createClient({ mode: 'rtc', codec: 'vp8' })
const remoteContainer = ref(null)

async function join () {
  await client.join(appId, channel, token, null)
  client.on('user-published', async (user, mediaType) => {
    await client.subscribe(user, mediaType)
    if (mediaType === 'video') {
      const remotePlayerContainer = document.createElement('div')
      remotePlayerContainer.id = user.uid.toString()
      remoteContainer.value.appendChild(remotePlayerContainer)
      user.videoTrack.play(remotePlayerContainer)
    }
    if (mediaType === 'audio') {
      user.audioTrack.play()
    }
  })
}
</script>

<style scoped>
.agora-demo button {
  margin-bottom: 1em;
}
</style>
