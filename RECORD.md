# Record

## 2024-09-05

### 1、创建项目

```shell
mkdir stars-ui && cd stars-ui && pnpm init
mkdir packages docs
```

### 2、.gitignore

```gitignore
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
dist
dist-ssr
*.local

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?

pnpm-lock.yaml
```

### 3、package.json

```json
{
  "name": "@xumeng03/monorepo",
  "private": "true",
  "description": "A Component Library for Vue 3",
  "scripts": {
    "preinstall": "npx only-allow pnpm",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "license": "ISC",
  "engines": {
    "node": ">=18"
  }
}
```

### 4、pnpm-workspace.yaml

```yaml
packages:
  - "packages/*"
  - "docs"
  - "play"
```

### 5、初始化

#### 5.1、docs

```shell
pnpm init
```

`docs`的`package.json`如下

```json
{
  "name": "docs",
  "private": "true",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

#### 5.2、packages

```shell
for i in components hooks stars-ui themes utils; do
    mkdir $i && cd $i
    pnpm init
    cd ..
done
```

`components`、`hooks`、`themes`、`utils`的`package.json`如下

```json
{
  "name": "@stars-ui/components",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

`stars-ui`的`package.json`如下

```json
{
  "name": "@xumeng03/stars-ui",
  "version": "1.0.0",
  "description": "A Component Library for Vue 3",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

#### 5.3、play

```shell
# 根目录执行
pnpm create vite play -template vue-ts
```

`play`的`package.json`如下

```json
{
  "name": "play",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc -b && vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "vue": "^3.4.37"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.1.2",
    "typescript": "^5.5.3",
    "vite": "^5.4.1",
    "vue-tsc": "^2.0.29"
  }
}
```

### 6、依赖安装

#### 6.1、根目录依赖

```shell
pnpm add -Dw vite
pnpm add -Dw typescript
```

```shell
pnpm add -w vue
pnpm add -w lodash-es
```

把`@xumeng03/stars-ui`引入作为全局依赖

```json
{
  "name": "@xumeng03/monorepo",
  "private": "true",
  "description": "A Component Library for Vue 3",
  "scripts": {
    "preinstall": "npx only-allow pnpm",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "license": "ISC",
  "engines": {
    "node": ">=18"
  },
  "devDependencies": {
    "typescript": "^5.5.3",
    "vite": "^5.4.1"
  },
  "dependencies": {
    "lodash-es": "^4.17.21",
    "vue": "^3.4.37",
    "@xumeng03/stars-ui": "workspace:*"
  },
  "workspaces": [
    "packages/*",
    "play",
    "docs"
  ]
}
```

#### 6.2、docs依赖

> 按需求添加，我这里目前没有依赖需要安装

#### 6.3、package子包依赖安装

> 按需求添加，我这里只是在@xumeng03/stars-ui里面引入@stars-ui/components、@stars-ui/hooks、@stars-ui/themes、@stars-ui/utils

```json
{
  "name": "@xumeng03/stars-ui",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "@stars-ui/components": "workspace:*",
    "@stars-ui/hooks": "workspace:*",
    "@stars-ui/themes": "workspace:*",
    "@stars-ui/utils": "workspace:*"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

#### 6.4、play依赖

```json
{
  "name": "play",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc -b && vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "vue": "^3.4.37"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.1.2",
    "typescript": "^5.5.3",
    "vite": "^5.4.1",
    "vue-tsc": "^2.0.29"
  }
}
```

#### 6.5、安装依赖

```shell
pnpm install
```

#### 6.6、测试Monorepo

```shell
cd play
pnpm run dev
```
