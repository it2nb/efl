<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'หน้าหลัก',
          to: './member'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'ข้อมูลการศึกษา',
          to: './member/education'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'ข้อมูลการทำงาน',
          to: './member/work'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'ข้อมูลผลงาน',
          to: './member/award'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'ระบบแฟ้มสะสมผลงานออนไลน์'
    }
  },

  mounted() {
    let loginuser = JSON.parse(sessionStorage.getItem('loginuser')) || {}
    if(loginuser.userType != 'Member') {
      window.location.replace('/')
    }
  },
}
</script>
