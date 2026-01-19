<template>
  <div class="main-container">
    
    <header class="top-header">
      <div class="top-header-content">
        <img src="/images/logo.png" alt="NWS" class="mini-logo" width="35" height="35" />
        <div class="top-header-text">
          <span class="system-name">ระบบอิเล็กทรอนิกส์สำหรับใช้ในการติดตามประเมินผลส่วนราชการ</span>
          <span class="agency-name">สำนักงานคณะกรรมการพัฒนาระบบราชการ</span>
        </div>
      </div>
    </header>

    <div class="login-page">
      <div class="global-overlay"></div>

      <section class="hero-section">
        <div class="hero-content">
          
          <div class="main-title">
            <h1>ระบบอิเล็กทรอนิกส์</h1>
            <h2>
              สำหรับใช้ในการติดตามประเมินผล<br>
              ส่วนราชการ
            </h2>
          </div>

          <div class="promo-container">
            <p class="promo-label">พื้นที่ประชาสัมพันธ์</p>
            <img src="/images/banner-login.png" alt="ศูนย์ข้อมูลข่าวสารของราชการ" class="promo-image" />
          </div>

        </div>
      </section>

      <section class="form-section">
        <div class="login-box">
          
          <div class="form-header">
            <img src="/images/logo.png" alt="NWS" class="form-logo" />
            <h3>เข้าสู่ระบบสำหรับเจ้าหน้าที่</h3>
          </div>

          <div class="field">
            <label>ชื่อผู้ใช้งาน/อีเมล</label>
            <input 
              v-model="username" 
              type="text" 
              placeholder="กรอกชื่อผู้ใช้งาน/อีเมล" 
            />
          </div>

          <div class="field">
            <label>รหัสผ่าน</label>
            <div class="password-input">
              <input
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                placeholder="กรอกรหัสผ่าน"
                @keyup.enter="submitLogin"
              />
              <button type="button" @click="showPassword = !showPassword" class="eye-btn">
                <img 
                  v-if="showPassword" 
                  src="/images/openeye.png" 
                  alt="Hide Password" 
                  class="eye-icon" 
                />
                <img 
                  v-else 
                  src="/images/closeeye.png" 
                  alt="Show Password" 
                  class="eye-icon" 
                />
              </button>
            </div>
          </div>

          <p v-if="errorMessage" class="error">{{ errorMessage }}</p>

          <button class="btn-primary" :disabled="loading" @click="submitLogin">
            {{ loading ? 'กำลังเข้าสู่ระบบ...' : 'เข้าสู่ระบบ' }}
          </button>

          <div class="divider">
            <span>หรือ</span>
          </div>

          <button class="btn-thaid">
            <img src="/images/thaid-logo.png" alt="ThaID Login" class="thaid-logo-img" />
            <span>เข้าสู่ระบบด้วย ThaID</span>
          </button>

          <div class="form-footer-links">
            <a href="#">ลืมรหัสผ่าน</a> | <a href="#">ลงทะเบียนเข้าใช้งาน</a>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const username = ref('')
const password = ref('')
const loading = ref(false)
const errorMessage = ref('')
const showPassword = ref(false)

const submitLogin = async () => {
  if (!username.value || !password.value) {
    errorMessage.value = 'กรุณากรอกชื่อผู้ใช้งานและรหัสผ่าน'
    return
  }
  loading.value = true
  errorMessage.value = ''
  try {
    // จำลองการเชื่อมต่อ API (รอ 1 วินาที)
    await new Promise(resolve => setTimeout(resolve, 1000))
    alert('เข้าสู่ระบบสำเร็จ')
  } catch (e) {
    errorMessage.value = 'เข้าสู่ระบบไม่สำเร็จ'
  } finally {
    loading.value = false
  }
}
</script>

<style scoped>
/* เรียกใช้ไฟล์ CSS ภายนอก */
@import "~/assets/login-design-02.css";
</style>