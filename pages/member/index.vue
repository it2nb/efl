<template>
  <div>
    <UserinfoData :userID="loginuser.userID" :updateTime="updateData" />
    <div class="mt-5 text-right">
      <v-btn small color="warning" @click="showEdit">แก้ไข</v-btn>
    </div>

    <div class="text-center">
      <v-dialog
        v-model="editdialog"
        width="1000"
        persistent
      >
        <UserinfoEdit :userID="loginuser.userID" :updateTime="updateEdit" @editStatus="editStatus" />
      </v-dialog>
    </div>
  </div>
</template>
<script>
import UserinfoData from '~/components/UserinfoData'
import UserinfoEdit from '~/components/UserinfoEdit'
export default {
  layout: 'memberLayout',

  components: {
    UserinfoData,
    UserinfoEdit,
  },

  data() {
    return {
      loginuser: {},
      editdialog: false,
      updateData: '',
      updateEdit: '',
    }
  },

  mounted() {
    this.loginuser = JSON.parse(sessionStorage.getItem('loginuser')) || {}
  },

  methods: {
    showEdit() {
      this.updateEdit = new Date().toString()
      this.editdialog = true
    },

    editStatus(data) {
      if(data === 'Success') {
        this.updateData = new Date().toString()
      }
      this.editdialog = false
    }
  }
}
</script>
