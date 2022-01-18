<template>
  <div>
    <v-row>
      <v-col class="text-center">
        <h1>เข้าสู่ระบบ</h1>
        <form @submit="Login">
          <v-text-field
            v-model="userName"
            label="ชื่อผู้ใช้"
            required
          ></v-text-field>
          <v-text-field
            v-model="userPassword"
            type="password"
            label="รหัสผ่าน"
            required
          ></v-text-field>

          <v-btn
            class="mr-4"
            type="submit"
          >
            เข้าสู่ระบบ
          </v-btn>
        </form>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import Swal from 'sweetalert2'
export default {
  data() {
    return {
      userName: '',
      userPassword: '',
    }
  },

  methods: {
    async Login(event) {
      event.preventDefault()
      let result = await this.$axios.$post('user.login.php', {
        userName: this.userName,
        userPassword: this.userPassword,
      })

      if(result.status === 'Success') {
        let user = result.data
        if(user.userStatus === 'Enable') {
          sessionStorage.setItem('loginuser', JSON.stringify(user))
          if(user.userType === 'Admin') {
            window.location.replace('./admin')
          } else if(user.userType === 'Member') {
            window.location.replace('./member')
          }
        } else {
          Swal.fire({
            title: 'ผิดพลาด',
            text: 'ชื่อผู้ใช้นี้ยังไม่ได้อนุญาตให้ใช้งาน',
            icon: 'warning'
          })
        }
      }
    }
  }
}
</script>
