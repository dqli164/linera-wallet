<template>
  <div>
    <p><strong>BE CAREFUL</strong></p>
    <p>
      Press this button will clear all accounts stored in CheCko including their
      public keys and private keys. Please make sure you already backup them
      correctly.
    </p>
  </div>
  <q-btn
    outline
    rounded
    label='Clear Accounts'
    @click='onClearAccountsClick'
    class='text-grey-6 bg-grey-3'
    :style='{
      width: "100%"
    }'
  />
</template>

<script setup lang='ts'>
import { notify, wallet } from 'src/localstores'

const _wallet = wallet.useWalletStore()
const notification = notify.useNotificationStore()

const onClearAccountsClick = () => {
  _wallet.reset()
  notification.pushNotification({
    Title: 'Clear Accounts',
    Message: 'Success clear all accounts.',
    Popup: true,
    Type: notify.NotifyType.Info
  })
}
</script>
