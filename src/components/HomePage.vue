<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

const navigateToLogin = () => {
  router.push('/login')
}

const navigateToRegister = () => {
  router.push('/register')
}
</script>

<template>
  <v-container class="fill-height d-flex align-center justify-center">
    <v-card class="pa-8" width="400" elevation="0" style="border-radius: 16px;">
      <v-card-title class="text-h5 text-center mb-6 font-weight-bold">欢迎使用 Roogoo</v-card-title>
      
      <v-card-text class="text-center mb-4">
        极简设计的 H5 应用模板
      </v-card-text>

      <v-card-actions class="flex-column">
        <v-btn 
          color="primary" 
          block 
          size="large"
          class="mb-4"
          @click="navigateToLogin"
          style="border-radius: 8px;"
        >
          登录
        </v-btn>
        
        <v-btn 
          variant="outlined" 
          block 
          size="large"
          @click="navigateToRegister"
          style="border-radius: 8px;"
        >
          注册
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<style scoped>
.fill-height {
  min-height: 100vh;
}
</style>