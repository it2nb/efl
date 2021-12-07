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
export default {
  data() {
    return {
      userName: '',
      userPassword: '',
    }
  },

  methods: {
    Login(event) {
      event.preventDefault()
      console.log('User =',this.userName)
      console.log('Pass =',this.userPassword)
    }
  }
}
</script>
