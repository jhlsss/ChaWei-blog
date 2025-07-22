---
title: vue3+ts项目中设置src别名@
date: 2025-7-21
tags: vue3
categories: vue
---

# vue3+ts项目中设置src别名@

## 1.修改`vite.config.ts`

```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve:{
    alias:{
      '@':path.resolve(__dirname,'src')
    }
  }
})
```

##  2.修改ts配置文件
ps：在`tsconfig.json`或者`tsconfig.app.json`里的`compilerOptions`配置

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```
