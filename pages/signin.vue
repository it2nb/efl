<template>
  <div>
    <v-row>
      <v-col  cols="12" md="5" class="mx-auto">
        <LoginForm />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import LoginForm from '~/components/LoginForm'
export default {
  components: {
    LoginForm,
  }
}
</script>
