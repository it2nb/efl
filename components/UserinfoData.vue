<template>
  <div>
    <v-card
      class="mx-auto"
    >
    <v-toolbar
      color="cyan"
      dark
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>ข้อมูลทั่วไป</v-toolbar-title>

      <v-spacer></v-spacer>
    </v-toolbar>

    <v-row>
      <v-col cols="12" md="6">
        <v-list three-line>
          <template>
            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>ชื่อ - สกุล</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoPrefix }} {{ userinfo.userinfoFullname }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>เพศ</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoGender }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>วันเกิด</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoBirthday }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>เป้าหมายในชีวิต</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoGoal }}
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
                  {{ userinfo.userinfoAddress }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>เบอร์โทรศัพท์</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoPhone }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Email</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoEmail }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Website</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoWebsite }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>ความสามารถพิเศษ</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoTalent }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>งานอดิเรก</v-list-item-title>
                <v-list-item-subtitle>
                  {{ userinfo.userinfoHobby }}
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>
          </template>
        </v-list>
      </v-col>
    </v-row>

  </v-card>
  </div>
</template>

<script>
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
console.log(result)
        if(result.status === 'Success') {
          this.userinfo = result.data
        }
      }
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
