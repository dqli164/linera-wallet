<template>
  <div class='row' :style='{ padding: "16px 0 8px 0" }'>
    <q-img
      src='~assets/CheCko.png'
      height='24px'
      width='160px'
      fit='contain'
      class='logo'
    />

    <q-space />
    <AccountList />
    <div
      class='text-brown-10 text-bold'
      :style='{
        margin: "10px 4px",
        fontSize: "16px",
      }'
      v-if='currentAddress'
    >
      {{ accountBalance.toFixed(2) }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { wallet } from 'src/localstores'

import AccountList from 'src/components/AccountList.vue'

const _wallet = wallet.useWalletStore()
const currentAddress = computed(() => _wallet.currentAddress)

const accountBalance = computed(() =>
  _wallet.accountBalance(undefined, undefined)
)
</script>
<style scoped lang="sass">
.logo
  margin: 12px 6px
</style>
