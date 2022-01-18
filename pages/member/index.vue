<template>
  <div>
    <h1>Member</h1>
    <UserinfoData :userID="loginuser.userID" />
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
