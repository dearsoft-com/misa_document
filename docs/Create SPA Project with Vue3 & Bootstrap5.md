# Create SPA Project with Vue3 & Bootstrap5

## Introduction

In this article, we will create a single page application project with Vue3 and Bootstrap5.

## Prerequisites

- Node.js
- NPM
- Vite

## Steps

### 1. Create a new project

We will use Vite to create a new project.  
First, open terminal and change directory to the workspace root.  

```bash
$ cd /path/to/workspace-root
```

Then, call NPM to create a new project, you will be asked to enter the project name, and select the framework.

```bash
$ npm create vite@latest
✔ Project name: · {project-name}
✔ Select a framework: › vue
✔ Select a variant: › javascript
```

After that, change directory to the project root, and install dependencies.

```bash
$ cd {project-name}
$ npm install
```

Now we have a new project with Vue3.

### 2. Set vite.config.js

In default settings, Vite will build the project to the `dist` directory, and all files would be directly under the `dist` directory.  
To make the project organized as other Dearsoft project, we need to change the hierarchy of the `dist` directory as below.

```
dist
├── css/client_ui
│   └── index-{hash}.css
├── images/client_ui
│   └── {image-file}
└── scripts/client_ui
    └── index-{hash}.js
```

To do this, we need to set the `vite.config.js` file.

```js
// vite.config.js
import { fileURLToPath } from 'url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },
  build: {
    rollupOptions: {
      output: {
        assetFileNames: (assetInfo) => {
          let ext = assetInfo.name?.split('.').at(1) ?? 'other'
          if (/png|jpe?g|svg|gif|tiff|bmp|ico/i.test(ext)) {
            ext = 'images/client_ui'
          } else if (ext == 'css') {
            ext = 'css/client_ui'
          }
          return `${ext}/[name]-[hash][extname]`
        },
        chunkFileNames: 'scripts/client_ui/[name]-[hash].js',
        entryFileNames: 'scripts/client_ui/[name]-[hash].js',
      }
    },
  },
})
```


### 3. Set environment variables

We need to set the environment variables for the project.  
First, create a `.env` file in the project root.

```
# .env
VITE_APP_SITE_TITLE="{site-title}"
VITE_APP_API_HOST="https://{api-host}"
```

**IMPORTANT:** For variables with `VITE_APP_` prefix, we can access them in the project with `import.meta.env.VITE_APP_{variable-name}`.


### 4. Install Bootstrap5

We will use Bootstrap5 for the UI framework.

```bash
$ npm install bootstrap
```

Then, import Bootstrap5 in the `main.js` file.

```js
// src/main.js
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap'
import '@/assets/style.css'
import { createApp } from 'vue'
import App from './App.vue'
//TODO: import router...

createApp(App).mount('#app')
```


### 5. Install vue-router

To build a single page application, we need to install vue-router.

```bash
$ npm install vue-router
```

Then, create a `router.js` file in the `src` directory.

```js
// src/router.js
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '@/views/HomeView.vue'

const title = import.meta.env.VITE_APP_SITE_TITLE
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    }
  ],
})
router.afterEach((to, _) => {
  document.title = to.meta.title ? `${to.meta.title} - ${title}` : title
})

export default router
```

_**NOTE:** We will create the `HomeView.vue` file later._

Then, import the router in the `main.js` file.

```js
// src/main.js
import { createApp } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap'
import '@/assets/style.css'
import App from './App.vue'
import router from './router'

createApp(App).use(router).mount('#app')
```


### 6. Create views

To separate views (called by router) and components (composing part of views), we will create a `views` directory in the `src` directory.

```bash
$ mkdir src/views
```

Then, create a `HomeView.vue` file in the `src/views` directory, and copy original code from `App.vue` to `HomeView.vue`.

```vue
<!-- src/views/HomeView.vue -->
<script setup>
import HelloWorld from '@/components/HelloWorld.vue'
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="@/assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
```

**NOTE:** Do not forget to change file path `./` to `@/`.

Then, change the `App.vue` file as below.

```vue
<!-- src/App.vue -->
<template>
  <RouterView />
</template>
```


### 7. Initialize git repository

To manage the project with git, we need to initialize git repository.

```bash
$ git init
```

If there are sensitive information in environment variables (such as API key), we need to add `.env` to `.gitignore` file.


### 8. Done

Now we have a single page application project with Vue3 and Bootstrap5.