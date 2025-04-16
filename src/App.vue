<template>
  <el-config-provider :locale="zhCn">
    <el-container class="app-container">
      <el-header class="app-header">
        <div class="header-content">
          <div class="logo">
            <el-icon :size="24" class="logo-icon"><Tools /></el-icon>
            <h1>工具站集合</h1>
          </div>
          <div class="header-right">
            <el-input
              v-model="searchQuery"
              placeholder="搜索工具..."
              class="search-input"
              :prefix-icon="Search"
              clearable
            />
            <el-switch
              v-model="isDark"
              inline-prompt
              :active-icon="Moon"
              :inactive-icon="Sunny"
              @change="toggleTheme"
            />
          </div>
        </div>
      </el-header>
      <el-main class="app-main">
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-config-provider>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Tools, Search, Moon, Sunny } from '@element-plus/icons-vue'
import zhCn from 'element-plus/dist/locale/zh-cn.mjs'

const searchQuery = ref('')
const isDark = ref(false)

const toggleTheme = () => {
  if (isDark.value) {
    document.documentElement.classList.add('dark')
    document.documentElement.setAttribute('data-theme', 'dark')
  } else {
    document.documentElement.classList.remove('dark')
    document.documentElement.removeAttribute('data-theme')
  }
}

onMounted(() => {
  // 检查系统主题偏好
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  if (prefersDark) {
    isDark.value = true
    document.documentElement.classList.add('dark')
    document.documentElement.setAttribute('data-theme', 'dark')
  }

  // 监听系统主题变化
  window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
    isDark.value = e.matches
    if (e.matches) {
      document.documentElement.classList.add('dark')
      document.documentElement.setAttribute('data-theme', 'dark')
    } else {
      document.documentElement.classList.remove('dark')
      document.documentElement.removeAttribute('data-theme')
    }
  })
})
</script>

<style>
:root {
  --bg-color: #ffffff;
  --text-color: #303133;
  --border-color: #dcdfe6;
  --card-bg: #ffffff;
  --card-border: #ebeef5;
  --hover-bg: #f5f7fa;
  --header-height: 60px;
  --primary-color: #409EFF;
  --success-color: #67C23A;
  --warning-color: #E6A23C;
  --danger-color: #F56C6C;
  --info-color: #909399;
}

:root[data-theme="dark"] {
  --bg-color: #1a1c1e;
  --text-color: #e1e3e6;
  --border-color: #2c2e30;
  --card-bg: #242628;
  --card-border: #2c2e30;
  --hover-bg: #2c2e30;
  --primary-color: #3a8ee6;
  --success-color: #5daf34;
  --warning-color: #cf9236;
  --danger-color: #dd6161;
  --info-color: #82848a;
}

.app-container {
  min-height: 100vh;
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: background-color 0.3s, color 0.3s;
}

.app-header {
  background-color: var(--card-bg);
  border-bottom: 1px solid var(--border-color);
  padding: 0 20px;
  height: var(--header-height);
  position: fixed;
  width: 100%;
  z-index: 1000;
  transition: background-color 0.3s, border-color 0.3s;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
}

.logo-icon {
  color: var(--primary-color);
  transition: color 0.3s;
}

.logo h1 {
  margin: 0;
  font-size: 20px;
  color: var(--text-color);
  transition: color 0.3s;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 20px;
}

.search-input {
  width: 300px;
}

.app-main {
  padding-top: calc(var(--header-height) + 20px);
  max-width: 1200px;
  margin: 0 auto;
}

/* 优化 Element Plus 的点击效果 */
.el-button,
.el-switch,
.el-input,
.el-card {
  transition: all 0.2s ease-in-out !important;
}

.el-button:active,
.el-switch:active,
.el-input:active,
.el-card:active {
  transform: scale(0.98) !important;
}

.el-button:hover,
.el-switch:hover,
.el-input:hover,
.el-card:hover {
  transform: translateY(-1px) !important;
}

@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    padding: 10px 0;
  }

  .header-right {
    width: 100%;
    justify-content: space-between;
  }

  .search-input {
    width: 200px;
  }
}
</style> 