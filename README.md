# bitget-task-skills

Bitget 交易任务模板 Skills — 兼容 Claude Code / Cursor / Codex 等 40+ Agent。

## 安装

```bash
# 安装全部 skills（Claude Code）
npx skills add duolaAmengweb3/bitget-task-skills --all -a claude-code

# 安装全部 skills（Cursor）
npx skills add duolaAmengweb3/bitget-task-skills --all -a cursor

# 安装单个 skill
npx skills add duolaAmengweb3/bitget-task-skills --skill sleep-mode -a claude-code
```

## 包含的 Skills

| Skill | 触发词 | 说明 |
|-------|--------|------|
| `/sleep-mode` | 睡觉模式、夜间守护、盯盘 | 持续监控价格，条件触发后自动执行交易 |
| `/event-mode` | 事件模式、异动、爆仓 | 检测市场异动事件，执行仓位调整或提醒 |
| `/copy-mode` | 复制模式、跟单、找交易员 | 筛选交易员、分配预算、执行跟单 |

## 前置条件

1. 安装 `bgtask` CLI：
   ```bash
   npm install -g @hunterweb303/bgtask
   ```

2. 配置 Bitget API Key 环境变量：
   ```bash
   export BITGET_API_KEY="your_api_key"
   export BITGET_SECRET_KEY="your_secret_key"
   export BITGET_PASSPHRASE="your_passphrase"
   ```

3. 验证环境：
   ```bash
   bgtask check
   ```

## 使用示例

```
/sleep-mode 盯 BTC，跌 2.5% 买 100U，稳健档
/event-mode BTC 异动时减仓 20%
/copy-mode 筛 30 天低回撤交易员，预算 500U
```

## 配合 MCP Server

可在 `.claude/mcp.json` 中同时配置官方 MCP Server 以获得更丰富的交互能力：

```json
{
  "mcpServers": {
    "bitget": {
      "command": "npx",
      "args": ["-y", "bitget-mcp-server"],
      "env": {
        "BITGET_API_KEY": "${BITGET_API_KEY}",
        "BITGET_SECRET_KEY": "${BITGET_SECRET_KEY}",
        "BITGET_PASSPHRASE": "${BITGET_PASSPHRASE}"
      }
    }
  }
}
```

## License

MIT
