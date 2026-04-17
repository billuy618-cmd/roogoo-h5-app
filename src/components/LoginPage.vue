<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const password = ref('')
const showPassword = ref(false)
const loading = ref(false)

const handleLogin = async () => {
  if (!email.value || !password.value) {
    return
  }
  
  loading.value = true
  // 模拟登录请求
  await new Promise(resolve => setTimeout(resolve, 1000))
  loading.value = false
  
  // 登录成功后跳转到首页
  router.push('/')
}

const navigateToRegister = () => {
  router.push('/register')
}

const navigateToHome = () => {
  router.push('/')
}
</script>

<template>
  <v-container class="fill-height d-flex align-center justify-center">
    <v-card class="pa-8" width="400" elevation="0" style="border-radius: 16px;">
      <v-btn
        icon
        variant="text"
        class="mb-4"
        @click="navigateToHome"
      >
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
      
      <v-card-title class="text-h5 text-center mb-6 font-weight-bold">登录 Roogoo</v-card-title>
      
      <v-card-text>
        <v-form @submit.prevent="handleLogin">
          <v-text-field
            v-model="email"
            label="邮箱"
            type="email"
            variant="outlined"
            class="mb-4"
            :rules="[v => !!v || '请输入邮箱']"
            required
            density="comfortable"
          />
          
          <v-text-field
            v-model="password"
            label="密码"
            :type="showPassword ? 'text' : 'password'"
            variant="outlined"
            class="mb-2"
            :rules="[v => !!v || '请输入密码']"
            required
            :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
            @click:append-inner="showPassword = !showPassword"
            density="comfortable"
          />
          
          <div class="text-right mb-6">
            <v-btn variant="text" size="small" color="primary">忘记密码？</v-btn>
          </div>
          
          <v-btn
            color="primary"
            block
            size="large"
            type="submit"
            :loading="loading"
            :disabled="!email || !password"
            style="border-radius: 8px;"
          >
            登录
          </v-btn>
        </v-form>
      </v-card-text>
      
      <v-card-actions class="justify-center mt-4">
        <span class="text-caption text-disabled">还没有账号？</span>
        <v-btn
          variant="text"
          size="small"
          color="primary"
          @click="navigateToRegister"
        >
          立即注册
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