<h3 align="center"> Komari Neko </h3>
<p align="center">
基于 Vue 3 + Vite + reka-ui + Tailwind CSS v4 构建的 Komari Monitor 主题（Neko 猫娘风格，Emerald 变体）
</p>

![preview](/docs/preview.png)

## 使用

1. 从 [Release 页面](https://github.com/nekomini88/komari-theme-Neko/releases) 下载最新的 `komari-theme-neko-build-*.zip` 文件
2. 登录 Komari Monitor 后，点击 `设置`，选择 `主题管理` 选项卡
3. 点击 `上传主题` 按钮，选择下载的 `komari-theme-neko-build-*.zip` 文件
4. 刷新页面，即可看到新的主题

## 环境要求

- Node.js: `^20.19.0` 或 `>=22.12.0`
- Bun: `>=1.2.0`

## 开发

```bash
# 安装依赖
bun install

# 启动开发服务器
bun run dev

# 代码检查
bun run lint
```

## 构建

```bash
# 类型检查 + 生产构建
bun run build

# 预览生产构建
bun run preview
```

构建产物：`dist/`（静态站点）与 `komari-theme-neko-build-<sha>.zip`（可上传到 Komari 的主题包）。

## 发布

```bash
bun run publish    # 同步提升 package.json 与 komari-theme.json 版本号并 git add
```

推送后 GitHub Actions（`release-on-version-bump.yml`）自动构建 zip 并创建 Release。

## 目录结构

```
komari-theme-Neko/
├── src/                # 主题源码（Vue 组件 / 样式）
├── public/images/      # 运行时静态资源
├── scripts/            # publish.ts 发布脚本、background*.frag 背景着色器
├── komari-theme.json   # 主题清单（名称 / 版本 / 可配置项）
├── docs/preview.png    # 预览图
└── package.json
```

## 技术栈

| 类别     | 技术                             |
| -------- | -------------------------------- |
| 框架     | Vue 3                            |
| 构建工具 | Vite 7                           |
| UI 组件  | reka-ui（shadcn-vue 风格组件）   |
| 样式方案 | Tailwind CSS v4 + tw-animate-css |
| 状态管理 | Pinia 3                          |
| 路由     | Vue Router 5                     |
| 提示系统 | vue-sonner（Toaster）            |
| 图标     | @iconify/vue                     |
| 图表     | vue-echarts                      |
| 3D 地球  | cobe                             |
| 实用工具 | @vueuse/core, dayjs              |
| 代码规范 | ESLint (@antfu/eslint-config)    |

## 鸣谢

- [Komari](https://github.com/komari-monitor/komari)
- [Komari Naive](https://github.com/tonyliuzj/komari-naive)
- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [reka-ui](https://reka-ui.com/)
- [Tailwind CSS](https://tailwindcss.com/)

## License

[MIT](./LICENSE)
