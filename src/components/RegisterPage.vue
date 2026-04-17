<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const verificationCode = ref('')
const password = ref('')
const confirmPassword = ref('')
const showPassword = ref(false)
const showConfirmPassword = ref(false)
const loading = ref(false)
const countdown = ref(0)
let timer: any = null

const handleRegister = async () => {
  if (!email.value || !verificationCode.value || !password.value || !confirmPassword.value) {
    return
  }
  
  if (password.value !== confirmPassword.value) {
    // 这里应该显示错误信息
    return
  }
  
  loading.value = true
  // 模拟注册请求
  await new Promise(resolve => setTimeout(resolve, 1000))
  loading.value = false
  
  // 注册成功后跳转到首页
  router.push('/')
}

const navigateToLogin = () => {
  router.push('/login')
}

const navigateToHome = () => {
  router.push('/')
}

const sendVerificationCode = () => {
  if (!email.value) {
    return
  }
  
  // 模拟发送验证码
  countdown.value = 60
  timer = setInterval(() => {
    countdown.value--
    if (countdown.value <= 0 && timer) {
      clearInterval(timer)
      timer = null
    }
  }, 1000)
}

// 清理定时器
import { onUnmounted } from 'vue'
onUnmounted(() => {
  if (timer) {
    clearInterval(timer)
  }
})
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
      
      <v-card-title class="text-h5 text-center mb-6 font-weight-bold">注册 Roogoo 账号</v-card-title>
      
      <v-card-text>
        <v-form @submit.prevent="handleRegister">
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
          
          <div class="d-flex align-center mb-4">
            <v-text-field
              v-model="verificationCode"
              label="验证码"
              variant="outlined"
              class="mr-2"
              :rules="[v => !!v || '请输入验证码']"
              required
              density="comfortable"
            />
            <v-btn
              color="primary"
              variant="outlined"
              :disabled="!email || countdown > 0"
              @click="sendVerificationCode"
              style="border-radius: 6px;"
            >
              {{ countdown > 0 ? `${countdown}s` : '发送验证码' }}
            </v-btn>
          </div>
          
          <v-text-field
            v-model="password"
            label="密码"
            :type="showPassword ? 'text' : 'password'"
            variant="outlined"
            class="mb-4"
            :rules="[v => !!v || '请输入密码']"
            required
            :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
            @click:append-inner="showPassword = !showPassword"
            density="comfortable"
          />
          
          <v-text-field
            v-model="confirmPassword"
            label="确认密码"
            :type="showConfirmPassword ? 'text' : 'password'"
            variant="outlined"
            class="mb-6"
            :rules="[
              v => !!v || '请确认密码',
              v => v === password || '密码不一致'
            ]"
            required
            :append-inner-icon="showConfirmPassword ? 'mdi-eye-off' : 'mdi-eye'"
            @click:append-inner="showConfirmPassword = !showConfirmPassword"
            density="comfortable"
          />
          
          <v-btn
            color="primary"
            block
            size="large"
            type="submit"
            :loading="loading"
            :disabled="!email || !verificationCode || !password || !confirmPassword || password !== confirmPassword"
            style="border-radius: 8px;"
          >
            注册
          </v-btn>
        </v-form>
      </v-card-text>
      
      <v-card-actions class="justify-center mt-4">
        <span class="text-caption text-disabled">已有账号？</span>
        <v-btn
          variant="text"
          size="small"
          color="primary"
          @click="navigateToLogin"
        >
          立即登录
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