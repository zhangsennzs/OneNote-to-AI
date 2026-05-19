# OneNote-to-AI
# 项目描述

---

## 一句话简介

```
在 Cursor / Claude 等 AI 工具中通过 MCP 读写 Microsoft OneNote，无需 Azure 注册，支持 Token 自动续期。含中文教程。
```

**英文版：**

```
Connect Microsoft OneNote to Cursor & MCP clients. No Azure signup. Browser auth with auto token refresh. Chinese docs included.
```

---

## 完整项目描述（用于 README 开头 / 项目介绍页）

### 项目名称

**OneNote MCP 接入方案**（onenote-mcp-local）

### 项目定位

将 **Microsoft OneNote** 与 **Model Context Protocol（MCP）** 生态打通，使开发者与知识工作者能在 **Cursor、Claude Desktop** 等 AI 工具中，用自然语言直接管理云端笔记，而无需在 IDE 与 OneNote 客户端之间反复切换。

### 解决的问题

- 官方未提供面向个人用户的「OneNote + Cursor」一键集成方案  
- 社区 npm 包存在 Azure 强依赖、包损坏、`npx` 兼容等问题  
- 设备码登录在 Windows 上易出现 localhost 拒绝连接、Token 无法保存  
- 仅保存 Access Token 时，约 1 小时即失效，需频繁重新登录  

本仓库在 [danosb/onenote-mcp](https://github.com/danosb/onenote-mcp) 基础上完成**生产可用化整理**，形成可复制、可迁移、文档齐全的方案。

### 核心能力

| 能力 | 说明 |
|------|------|
| 笔记本管理 | 列出笔记本、分区、页面 |
| 内容读取 | 获取页面 HTML，供 AI 摘要、整理、出题 |
| 搜索与创建 | 跨笔记搜索、在指定分区创建新页面 |
| MCP 标准接入 | stdio 传输，兼容 Cursor / Claude Desktop 等 |
| 免 Azure 注册 | 使用 Microsoft Graph Explorer 公共客户端 + 浏览器登录 |
| Token 自动续期 | `auth-manager.mjs` + MSAL 本地缓存，静默刷新 Access Token |

### 技术栈

- **运行时**：Node.js LTS  
- **协议**：Model Context Protocol（MCP）  
- **API**：Microsoft Graph OneNote API  
- **认证**：`@azure/msal-node`（交互式登录 + Refresh Token 持久化）  
- **上游**：danosb/onenote-mcp + MCP TypeScript SDK 1.12.0  

### 适用人群

- 使用 OneNote 记录学习/工作笔记，并希望在 **Cursor Agent** 中整理、检索、生成大纲的用户  
- 需要把笔记上下文接入 AI 工作流（复习、会议纪要、知识库问答）的开发者  
- 希望在多台电脑间复制同一套 MCP 配置的团队或个人  

### 使用方式概览

1. 克隆本仓库，在 `onenote-mcp/` 目录执行 `npm install`  
2. 配置 MCP 客户端的 `mcp.json`（指向 `onenote-mcp.mjs`）  
3. 执行 `npm run auth` 完成浏览器登录  
4. 在 AI 对话中说：「请列出我的 OneNote 笔记本」等  

详细步骤见 `onenote-mcp/ONENOTE-MCP-教程.md`，换机见 `新电脑5分钟检查清单.md`。

### 开源与致谢

- 核心逻辑基于 [danosb/onenote-mcp](https://github.com/danosb/onenote-mcp)（MIT）  
- 本仓库贡献：认证续期、SDK 固定版本、权限修正、中文文档与排错指南  

---
