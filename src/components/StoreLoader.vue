<template>
  <div class='row q-pa-md q-gutter-md'>
    <q-space />
    <div class='text-center'>
      <q-img :src='cheCkoLogo' width='240px' />
      <q-card :style='{height: "160px"}' flat>
        <q-inner-loading
          :showing='loading'
          class='text-red-4'
        >
          <q-spinner-facebook size='80px' />
        </q-inner-loading>
      </q-card>
    </div>
    <q-space />
  </div>
</template>

<script setup lang='ts'>
import { onMounted, ref } from 'vue'
import { useRouter } from 'vue-router'
import { wallet, persistentsetting, oneshotsetting } from 'src/localstores'

import cheCkoLogo from 'src/assets/CheCko.png'

const _wallet = wallet.useWalletStore()
const _persistentsetting = persistentsetting.useSettingStore()
const _oneshotsetting = oneshotsetting.useSettingStore()
const router = useRouter()
const loading = ref(true)

onMounted(() => {
  _persistentsetting.load(() => {
    _wallet.loadPassword(() => {
      loading.value = false
      if (_wallet.initialized) {
        void router.push({ path: _oneshotsetting.extensionMode ? '/extension/recovery' : '/recovery' })
      } else {
        void router.push({ path: _oneshotsetting.extensionMode ? '/extension/onboarding' : '/onboarding' })
      }
    })
  })
})
</script>
