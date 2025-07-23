# Element Plus

文章参考：[官方文档](https://element-plus.org/)，[GitHub 仓库](https://github.com/element-plus/element-plus)，[组件示例](https://element-plus.org/en-US/component/button.html)[主题生成器](https://element-plus.org/en-US/theme-editor.html)

[TOC]

## 介绍

Element Plus 是一套基于 Vue 3 的桌面端组件库，由饿了么前端团队开发并开源。它提供了丰富的 UI 组件，帮助开发者快速构建企业级中后台产品。

### 特点

- **全面的组件**：包含按钮、表单、表格、弹窗等 50+ 常用组件
- **主题定制**：支持通过 SCSS 变量轻松定制主题
- **国际化**：内置多语言支持
- **TypeScript**：完全使用 TypeScript 开发，提供完整的类型定义
- **响应式**：完美适配各种屏幕尺寸

## 安装

### 使用 npm 或 yarn 安装

```bash
npm install element-plus
# 或
yarn add element-plus
```

### 完整引入

```javascript
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

### 按需引入

推荐使用 unplugin-vue-components 进行按需自动引入：

```bash
npm install -D unplugin-vue-components unplugin-auto-import
```

然后在 vite 或 webpack 配置中添加：

```javascript
// vite.config.ts
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default {
  plugins: [
    // ...
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
}
```

## 快速开始

### 基础示例

```vue
<template>
  <el-button type="primary" @click="handleClick">主要按钮</el-button>
  <el-alert title="成功提示" type="success" show-icon />
</template>

<script setup>
const handleClick = () => {
  ElMessage.success('按钮被点击了')
}
</script>
```

### 主题定制

1. 创建主题文件 `styles/element/index.scss`:

```scss
// 覆盖变量
@forward 'element-plus/theme-chalk/src/common/var.scss' with (
  $colors: (
    'primary': (
      'base': #409eff,
    ),
  )
);

// 导入所有样式
@use 'element-plus/theme-chalk/src/index.scss' as *;
```

2. 在入口文件中导入:

```javascript
import './styles/element/index.scss'
```

## 常用组件

### 表单组件

#### 输入框

```vue
<template>
  <el-input v-model="input" placeholder="请输入内容" />
</template>

<script setup>
import { ref } from 'vue'

const input = ref('')
</script>
```

#### 选择器

```vue
<template>
  <el-select v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value"
    />
  </el-select>
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const options = [
  { value: 'option1', label: '选项1' },
  { value: 'option2', label: '选项2' },
]
</script>
```

### 数据展示

#### 表格

```vue
<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="date" label="日期" width="180" />
    <el-table-column prop="name" label="姓名" width="180" />
    <el-table-column prop="address" label="地址" />
  </el-table>
</template>

<script setup>
const tableData = [
  { date: '2016-05-03', name: '王小虎', address: '上海市普陀区金沙江路 1518 弄' },
  { date: '2016-05-02', name: '王小虎', address: '上海市普陀区金沙江路 1518 弄' },
]
</script>
```

#### 分页

```vue
<template>
  <el-pagination
    v-model:current-page="currentPage"
    :page-size="100"
    layout="prev, pager, next"
    :total="1000"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentPage = ref(1)
</script>
```

### 反馈组件

#### 消息提示

```javascript
// 在组件中调用
ElMessage.success('成功消息')
ElMessage.error('错误消息')
ElMessage.warning('警告消息')
```

#### 对话框

```vue
<template>
  <el-button type="text" @click="dialogVisible = true">点击打开 Dialog</el-button>

  <el-dialog v-model="dialogVisible" title="提示" width="30%">
    <span>这是一段信息</span>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script setup>
import { ref } from 'vue'

const dialogVisible = ref(false)
</script>
```

## 高级用法

### 自定义主题

1. 安装 SCSS:

```bash
npm install sass -D
```

2. 创建主题文件 `src/styles/element/index.scss`:

```scss
@use "element-plus/theme-chalk/src/index" as *;

// 自定义变量
@forward "element-plus/theme-chalk/src/common/var.scss" with (
  $colors: (
    "primary": (
      "base": #27ba9b,
    ),
    "success": (
      "base": #1dc779,
    ),
    "warning": (
      "base": #ffb302,
    ),
    "danger": (
      "base": #e26237,
    ),
    "error": (
      "base": #cf4444,
    ),
  )
);
```

3. 在 `vite.config.ts` 中配置:

```javascript
export default defineConfig({
  css: {
    preprocessorOptions: {
      scss: {
        additionalData: `@use "@/styles/element/index.scss" as *;`,
      },
    },
  },
})
```

### 国际化

```javascript
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import zhCn from 'element-plus/dist/locale/zh-cn.mjs'
import 'element-plus/dist/index.css'

const app = createApp(App)
app.use(ElementPlus, {
  locale: zhCn,
})
```

### 全局配置

```javascript
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'

const app = createApp(App)
app.use(ElementPlus, { 
  size: 'large',
  zIndex: 3000
})
```

## 最佳实践

### 表单验证

```vue
<template>
  <el-form :model="ruleForm" :rules="rules" ref="formRef">
    <el-form-item label="活动名称" prop="name">
      <el-input v-model="ruleForm.name"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm">提交</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
import { ref } from 'vue'

const formRef = ref()
const ruleForm = ref({
  name: ''
})

const rules = {
  name: [
    { required: true, message: '请输入活动名称', trigger: 'blur' },
    { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
  ]
}

const submitForm = () => {
  formRef.value.validate((valid) => {
    if (valid) {
      alert('提交成功!')
    } else {
      console.log('验证失败')
      return false
    }
  })
}
</script>
```

### 表格与分页

```vue
<template>
  <el-table :data="tableData" v-loading="loading">
    <el-table-column prop="date" label="日期" />
    <el-table-column prop="name" label="姓名" />
    <el-table-column prop="address" label="地址" />
  </el-table>
  
  <el-pagination
    v-model:current-page="currentPage"
    :page-size="pageSize"
    layout="total, sizes, prev, pager, next, jumper"
    :total="total"
    @size-change="handleSizeChange"
    @current-change="handleCurrentChange"
  />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { getTableData } from '@/api/table'

const loading = ref(false)
const tableData = ref([])
const currentPage = ref(1)
const pageSize = ref(10)
const total = ref(0)

const fetchData = async () => {
  try {
    loading.value = true
    const res = await getTableData({
      page: currentPage.value,
      size: pageSize.value
    })
    tableData.value = res.data.list
    total.value = res.data.total
  } finally {
    loading.value = false
  }
}

const handleSizeChange = (val) => {
  pageSize.value = val
  fetchData()
}

const handleCurrentChange = (val) => {
  currentPage.value = val
  fetchData()
}

onMounted(() => {
  fetchData()
})
</script>
```

## 常见问题

### 样式冲突

如果遇到样式冲突，可以使用命名空间：

```javascript
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/theme-chalk/src/index.scss'

const app = createApp(App)
app.use(ElementPlus, { namespace: 'ep' })
```

然后组件使用 `ep-` 前缀：

```vue
<template>
  <ep-button type="primary">主要按钮</ep-button>
</template>
```

### CDN 引入

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <!-- 引入样式 -->
  <link rel="stylesheet" href="https://unpkg.com/element-plus/dist/index.css">
</head>
<body>
  <div id="app">
    <el-button type="primary">主要按钮</el-button>
  </div>
  
  <!-- 引入 Vue 和 Element Plus -->
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <script src="https://unpkg.com/element-plus"></script>
  
  <script>
    const { createApp } = Vue
    
    const app = createApp({
      // 选项
    })
    
    app.use(ElementPlus)
    app.mount('#app')
  </script>
</body>
</html>
```

