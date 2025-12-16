# XYinAPI 文档站

基于 [VitePress](https://vitepress.dev/) 构建的 XYinAPI 文档网站，提供文档格式转换服务的 API 文档。

## 简介

XYinAPI 是一个强大、高效、安全的文档格式转换 API 服务。本仓库为其官方文档站点源码。

## 后端服务

文档站依赖于后端 API 服务：[LOS-servies](https://github.com/rontowerdragonsingingZi/LOS-servies)

## 本地开发

```bash
# 安装依赖
npm install

# 启动开发服务器
npx vitepress dev docs

# 构建生产版本
npm run docs:build
```

## 项目结构

```
VitePress/
├── docs/
│   ├── .vitepress/    # VitePress 配置
│   ├── api/           # API 文档
│   ├── en/            # 英文文档
│   ├── public/        # 静态资源
│   └── *.md           # 文档页面
└── package.json
```

## 相关链接

- API 服务：https://vitepress.xyin.online
- 后端仓库：https://github.com/rontowerdragonsingingZi/LOS-servies

## License

ISC
