<template>
  <div class="home">
    <div class="section-title">
      <h2>工具分类</h2>
      <p>选择你需要的工具类型</p>
    </div>
    
    <div class="category-list">
      <div class="category-grid">
        <div 
          v-for="category in categories" 
          :key="category.id"
          class="category-card" 
          :class="{ 'is-active': selectedCategory?.id === category.id }"
          @click="selectCategory(category)"
        >
          <div class="category-content">
            <div class="icon-wrapper" :class="{ 'is-active': selectedCategory?.id === category.id }">
              <el-icon :size="32">
                <component :is="category.icon" />
              </el-icon>
            </div>
            <span class="category-name">{{ category.name }}</span>
          </div>
        </div>
      </div>
    </div>

    <div class="section-title">
      <h2>工具列表</h2>
      <p>{{ selectedCategory ? `当前分类：${selectedCategory.name}` : '所有工具' }}</p>
    </div>

    <div class="tool-list">
      <div class="tool-grid">
        <div 
          v-for="tool in filteredTools" 
          :key="tool.id"
          class="tool-card" 
          @click="openTool(tool)"
        >
          <div class="tool-content">
            <div class="tool-icon" :style="{ backgroundColor: tool.color }">
              <el-icon :size="32">
                <component :is="tool.icon" />
              </el-icon>
            </div>
            <div class="tool-info">
              <h3>{{ tool.name }}</h3>
              <p>{{ tool.description }}</p>
              <div class="tool-tags">
                <el-tag size="small" :type="tool.tagType">{{ getCategoryName(tool.categoryId) }}</el-tag>
                <el-tag size="small" type="success" v-if="tool.isNew">新上线</el-tag>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { 
  Document, 
  Picture, 
  Timer, 
  Reading, 
  House,
  Monitor,
  Camera,
  Calendar,
  Notebook,
  ShoppingCart,
  Connection,
  Setting,
  Upload
} from '@element-plus/icons-vue'

const selectedCategory = ref(null)

const categories = [
  { id: 1, name: '开发工具', icon: 'Monitor' },
  { id: 2, name: '设计工具', icon: 'Picture' },
  { id: 3, name: '效率工具', icon: 'Timer' },
  { id: 4, name: '学习工具', icon: 'Reading' },
  { id: 5, name: '生活工具', icon: 'House' }
]

const tools = [
  {
    id: 1,
    name: 'Mermaid AI',
    description: 'AI 智能生成 Mermaid 图表，支持流程图、类图、时序图等',
    icon: 'DataLine',
    color: '#409EFF',
    tagType: 'primary',
    isNew: true,
    url: 'http://49.235.121.253:9999/',
    categoryId: 1
  },
  {
    id: 2,
    name: '小鹅问问',
    description: '智能问答助手，提供专业的知识解答',
    icon: 'ChatDotRound',
    color: '#67C23A',
    tagType: 'success',
    isNew: true,
    url: 'http://49.235.121.253:9080/',
    categoryId: 3
  },
  {
    id: 3,
    name: '开发者简报',
    description: '给软件开发者准备的优质简报，每日阅读 10分钟',
    icon: 'Reading',
    color: '#E6A23C',
    tagType: 'warning',
    isNew: true,
    url: 'https://news.nilh2a2.dev/',
    categoryId: 4
  },
  {
    id: 4,
    name: 'JSON 格式化',
    description: '在线 JSON 格式化工具，支持 JSON 验证和压缩',
    icon: 'Document',
    color: '#409EFF',
    tagType: 'primary',
    isNew: true,
    url: 'https://www.json.cn/',
    categoryId: 1
  },
  {
    id: 5,
    name: 'TinyPNG',
    description: '智能图片压缩工具，保持图片质量的同时大幅减小文件大小',
    icon: 'Picture',
    color: '#67C23A',
    tagType: 'success',
    isNew: false,
    url: 'https://tinypng.com/',
    categoryId: 2
  },
  {
    id: 6,
    name: 'Google 日历',
    description: '功能强大的在线日历工具，支持日程管理和团队协作',
    icon: 'Calendar',
    color: '#E6A23C',
    tagType: 'warning',
    isNew: true,
    url: 'https://calendar.google.com/',
    categoryId: 3
  },
  {
    id: 7,
    name: '语雀',
    description: '专业的云端知识库，支持 Markdown 和团队协作',
    icon: 'Notebook',
    color: '#F56C6C',
    tagType: 'danger',
    isNew: false,
    url: 'https://www.yuque.com/',
    categoryId: 4
  },
  {
    id: 8,
    name: 'Todoist',
    description: '智能任务管理工具，支持多平台同步和团队协作',
    icon: 'ShoppingCart',
    color: '#909399',
    tagType: 'info',
    isNew: true,
    url: 'https://todoist.com/',
    categoryId: 5
  },
  {
    id: 9,
    name: 'Speedtest',
    description: '全球知名的网络速度测试工具，提供详细的网络性能分析',
    icon: 'Connection',
    color: '#409EFF',
    tagType: 'primary',
    isNew: false,
    url: 'https://www.speedtest.net/',
    categoryId: 3
  }
]

const filteredTools = computed(() => {
  if (!selectedCategory.value) return tools
  return tools.filter(tool => tool.categoryId === selectedCategory.value.id)
})

const selectCategory = (category) => {
  selectedCategory.value = selectedCategory.value?.id === category.id ? null : category
}

const openTool = (tool) => {
  window.open(tool.url, '_blank')
}

const getCategoryName = (categoryId) => {
  return categories.find(c => c.id === categoryId)?.name || '未知分类'
}
</script>

<style scoped>
.home {
  padding: 20px;
  background-color: var(--bg-color);
  min-height: 100vh;
}

.section-title {
  margin-bottom: 30px;
  text-align: center;
}

.section-title h2 {
  margin: 0;
  font-size: 24px;
  color: var(--text-color);
}

.section-title p {
  margin: 8px 0 0;
  color: var(--text-color);
  opacity: 0.7;
  font-size: 14px;
}

.category-list {
  margin-bottom: 40px;
}

.category-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.category-card {
  cursor: pointer;
  transition: all 0.3s;
  border: 1px solid var(--card-border);
  border-radius: 4px;
  background-color: var(--card-bg);
  width: 200px;
  height: 150px;
  display: flex;
  flex-direction: column;
  position: relative;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.category-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  background-color: var(--hover-bg);
}

.category-card.is-active {
  border-color: var(--primary-color);
  background-color: rgba(64, 158, 255, 0.05);
}

.category-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  height: 100%;
  box-sizing: border-box;
}

.icon-wrapper {
  width: 64px;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--hover-bg);
  border-radius: 16px;
  transition: all 0.3s;
  color: var(--text-color);
  margin-bottom: 15px;
}

.icon-wrapper.is-active {
  background-color: var(--primary-color);
  color: white;
}

.category-name {
  font-size: 14px;
  color: var(--text-color);
  transition: color 0.3s;
  text-align: center;
}

.category-card.is-active .category-name {
  color: var(--primary-color);
  font-weight: 500;
}

.tool-list {
  margin-top: 20px;
}

.tool-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.tool-card {
  cursor: pointer;
  transition: all 0.3s;
  border: 1px solid var(--card-border);
  border-radius: 4px;
  background-color: var(--card-bg);
  width: 300px;
  height: 120px;
  position: relative;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.tool-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  background-color: var(--hover-bg);
}

.tool-content {
  display: flex;
  align-items: flex-start;
  gap: 15px;
  height: 100%;
  padding: 15px;
  box-sizing: border-box;
}

.tool-icon {
  flex-shrink: 0;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  color: white;
  transition: all 0.3s;
}

.tool-card:hover .tool-icon {
  transform: rotate(10deg) scale(1.1);
}

.tool-info {
  flex: 1;
  min-width: 0;
  overflow: hidden;
}

.tool-info h3 {
  margin: 0;
  font-size: 16px;
  color: var(--text-color);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.tool-info p {
  margin: 8px 0;
  font-size: 12px;
  color: var(--text-color);
  opacity: 0.7;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  min-height: 36px;
}

.tool-tags {
  margin-top: 8px;
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

@media (max-width: 768px) {
  .category-card {
    width: calc(50% - 10px);
  }

  .tool-card {
    width: 100%;
  }

  .section-title h2 {
    font-size: 20px;
  }

  .category-content {
    padding: 15px;
  }

  .icon-wrapper {
    width: 48px;
    height: 48px;
  }

  .tool-content {
    gap: 10px;
    padding: 12px;
  }

  .tool-icon {
    width: 40px;
    height: 40px;
  }

  .tool-info p {
    font-size: 11px;
    min-height: 33px;
  }
}
</style>