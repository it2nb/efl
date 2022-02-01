<template>
  <div>
    <UserinfoData :userID="loginuser.userID" />
    <div class="mt-5 text-right">
      <v-btn small color="warning">แก้ไข</v-btn>
    </div>
  </div>
</template>
<script>
import UserinfoData from '~/components/UserinfoData'
export default {
  layout: 'memberLayout',

  components: {
    UserinfoData,
  },

  data() {
    return {
      loginuser: {}
    }
  },

  mounted() {
    this.loginuser = JSON.parse(sessionStorage.getItem('loginuser')) || {}
  }
}
</script>
