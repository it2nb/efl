<template>
  <div>

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
