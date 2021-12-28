<template>
  <div>
    <v-row>
      <v-col  cols="12" md="5" class="mx-auto">
        <SignupForm @getSignup="Signup" />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import SignupForm from '~/components/SignupForm'
import Swal from 'sweetalert2'
export default {
  components: {
    SignupForm,
  },

  methods: {
    async Signup(data) {
      let userInsert = await this.$axios.$post(
        'user.insert.php', {
          userName: data.userName,
          userPassword: data.userPassword,
          userType: 'Member',
          userStatus: 'Enable'
      })

      if(userInsert.status === 'Success') {
        let userID = userInsert.data.userID
        let userinfoInsert = await this.$axios.$post(
          'userinfo.insert.php', {
            userID: userID,
            userinfoFullname: data.userinfoFullname,
            userinfoPhone: data.userinfoPhone,
            userinfoEmail: data.userinfoEmail
        })

        if(userinfoInsert.status === 'Success') {
          Swal.fire({
            title: 'สำเร็จ',
            text: 'ยินดีต้อนรับเป็นสมาชิกระบบแฟ้มสะสมผลงาน',
            icon: 'success'
          }).then(()=>{
            window.location.replace('./signin')
          })
        } else {
          Swal.fire({
            title: 'ผิดพลาด',
            text: '**บันทึกข้อมูลไม่สำเร็จ',
            icon: 'error'
          })
        }
      } else {
        Swal.fire({
          title: 'ผิดพลาด',
          text: '*บันทึกข้อมูลไม่สำเร็จ',
          icon: 'error'
        })
      }
    }
  }
}
</script>
