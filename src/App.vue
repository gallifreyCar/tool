<template>
  <el-container class="app-container">
    <el-header class="app-header">
      <div class="header-content">
        <div class="logo">
          <el-icon :size="24"><Tools /></el-icon>
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
</template>

<script setup>
import { ref } from 'vue'
import { Tools, Search, Moon, Sunny } from '@element-plus/icons-vue'

const searchQuery = ref('')
const isDark = ref(false)

const toggleTheme = () => {
  document.documentElement.classList.toggle('dark')
}
</script>

<style>
:root {
  --primary-color: #409EFF;
  --header-height: 60px;
  --header-bg: #fff;
  --text-color: #333;
  --border-color: #dcdfe6;
}

.dark {
  --header-bg: #1f1f1f;
  --text-color: #fff;
  --border-color: #4c4d4f;
}

.app-container {
  min-height: 100vh;
}

.app-header {
  background-color: var(--header-bg);
  border-bottom: 1px solid var(--border-color);
  padding: 0 20px;
  height: var(--header-height);
  position: fixed;
  width: 100%;
  z-index: 1000;
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

.logo h1 {
  margin: 0;
  font-size: 20px;
  color: var(--text-color);
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