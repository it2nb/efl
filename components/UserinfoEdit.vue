<template>
  <div>
    <v-card
      class="mx-auto"
    >
    <v-toolbar
      color="warning"
      dark
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>แก้ไขข้อมูลทั่วไป</v-toolbar-title>

      <v-spacer></v-spacer>
    </v-toolbar>

    <form @submit.prevent="editUserinfo">
      <v-row>
        <v-col cols="12" md="6">
          <v-list three-line>
            <template>
              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>คำนำหน้าชื่อ</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-select
                      v-model="userinfo.userinfoPrefix"
                      :items="[
                        'นาย',
                        'นาง',
                        'นางสาว'
                      ]"
                    ></v-select>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>ชื่อ - สกุล</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoFullname"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>เพศ</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-select
                      v-model="userinfo.userinfoGender"
                      :items="['ชาย', 'หญิง']"
                    ></v-select>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>วันเกิด</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoBirthday"
                      type="date"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>เป้าหมายในชีวิต</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-textarea
                      v-model="userinfo.userinfoGoal"
                      rows="5"
                    ></v-textarea>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>
            </template>
          </v-list>
        </v-col>
        <v-col cols="12" md="6">
          <v-list three-line>
            <template>
              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>ที่อยู่</v-list-item-title>
                  <v-list-item-subtitle>
                    <textarea
                      v-model="userinfo.userinfoAddress"
                      rows="3"
                    ></textarea>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>เบอร์โทรศัพท์</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoPhone"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>Email</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoEmail"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>Website</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoWebsite"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>ความสามารถพิเศษ</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoTalent"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>งานอดิเรก</v-list-item-title>
                  <v-list-item-subtitle>
                    <v-text-field
                      v-model="userinfo.userinfoHobby"
                    ></v-text-field>
                  </v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>
            </template>
          </v-list>
        </v-col>
      </v-row>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          color="warning"
          type="submit"
        >แก้ไข</v-btn>
        <v-btn
          @click="cancel"
        >ยกเลิก</v-btn>
      </v-card-actions>
    </form>

  </v-card>
  </div>
</template>

<script>
import Swal from 'sweetalert2'
export default {
  props: {
    userID: {
      type: String,
      default: null
    },
    updateTime: {
      type: String,
      default: new Date().toString()
    }
  },

  data() {
    return {
      userinfo: {},
    }
  },

  async mounted() {
    await this.getUserinfo()
  },

  methods: {
    async getUserinfo() {
      if(this.userID) {
        let result = await this.$axios.$get('userinfo.php', {
          params: {
            userID: this.userID
          }
        })

        if(result.status === 'Success') {
          this.userinfo = result.data
        }
      }
    },

    async editUserinfo() {
      let result = await this.$axios.$post('userinfo.update.php', this.userinfo)

      if(result.status === 'Success') {
        Swal.fire({
          title: 'สำเร็จ',
          text: 'แก้ไขข้อมูลสำเร็จ',
          icon: 'success'
        }).then(()=> {
          this.$emit('editStatus', 'Success')
        })
      } else {
        Swal.fire({
          title: 'ผิดพลาด',
          text: 'แก้ไขข้อมูลไม่สำเร็จ',
          icon: 'error'
        }).then(()=> {
          this.$emit('editStatus', 'Fail')
        })
      }
    },

    cancel() {
      this.$emit('editStatus', 'False')
    }
  },

  watch: {
    async userID() {
      await this.getUserinfo()
    },

    async updateTime() {
      await this.getUserinfo()
    }
  }
}
</script>
