<template>
  <div>
    <v-row>
      <v-col class="text-center">
        <h1>สมัครสมาชิก</h1>
        <form @submit="Signup">
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
          <v-text-field
            v-model="cuserPassword"
            type="password"
            label="ยืนยันรหัสผ่าน"
            required
          ></v-text-field>
          <hr>
          <v-text-field
            v-model="userinfoFullname"
            label="ชื่อ - สกุล"
            required
          ></v-text-field>
          <v-text-field
            v-model="userinfoPhone"
            label="เบอร์โทรศัพท์"
            required
          ></v-text-field>
          <v-text-field
            v-model="userinfoEmail"
            label="Email"
            required
          ></v-text-field>

          <v-btn
            class="mr-4"
            type="submit"
          >
            สมัคร
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
      cuserPassword: '',
      userinfoFullname: '',
      userinfoPhone: '',
      userinfoEmail: '',
    }
  },

  methods: {
    async Signup(event) {
      event.preventDefault()
      if(this.userPassword === this.cuserPassword) {
        this.$emit('getSignup', {
          userName: this.userName,
          userPassword: this.userPassword,
          userinfoFullname: this.userinfoFullname,
          userinfoPhone: this.userinfoPhone,
          userinfoEmail: this.userinfoEmail,
        })
      } else {
        Swal.fire({
          title: 'ผิดพลาด',
          text: 'รหัสผ่านไม่ตรงกัน',
          icon: 'warning'
        })
      }
    }
  }
}
</script>
