# 睡觉模式示例

## 场景 1: 夜间抄底（带完整风控）

"今晚盯 BTC，跌 3% 买 200U，波动超 8% 别追，最多 2 次，冷却 1 小时，稳健档，先 dry-run"

```bash
bgtask run sleep-mode \
  --symbol BTCUSDT \
  --trigger-type price_drop \
  --trigger-value 3 \
  --action buy \
  --amount 200 \
  --risk-profile conservative \
  --max-triggers 2 \
  --cooldown 3600 \
  --volatility-guard 8 \
  --duration 28800 \
  --dry-run
```

确认 dry-run 效果后，去掉 `--dry-run` 放后台正式运行：

```bash
bgtask run sleep-mode \
  --symbol BTCUSDT \
  --trigger-type price_drop \
  --trigger-value 3 \
  --action buy \
  --amount 200 \
  --risk-profile conservative \
  --max-triggers 2 \
  --cooldown 3600 \
  --volatility-guard 8 \
  --confirm \
  --daemon
```

## 场景 2: 涨幅止盈

"盯着 ETH，涨 5% 卖出 200U，最多触发 2 次"

```bash
bgtask run sleep-mode \
  --symbol ETHUSDT \
  --trigger-type price_rise \
  --trigger-value 5 \
  --action sell \
  --amount 200 \
  --max-triggers 2 \
  --cooldown 1800 \
  --daemon
```

## 场景 3: 仅提醒模式

"帮我看着 SOL，跌 3% 提醒我就好"

```bash
bgtask run sleep-mode \
  --symbol SOLUSDT \
  --trigger-type price_drop \
  --trigger-value 3 \
  --action alert_only \
  --daemon
```

## 场景 4: 多币种并行监控

同时监控多个币种，放到后台并行运行：

```bash
# 先启动 daemon
bgtask daemon start

# BTC 跌 3% 买入
bgtask run sleep-mode --symbol BTCUSDT --trigger-value 3 --amount 200 --confirm --daemon

# ETH 跌 2% 买入
bgtask run sleep-mode --symbol ETHUSDT --trigger-value 2 --amount 150 --confirm --daemon

# SOL 跌 5% 买入
bgtask run sleep-mode --symbol SOLUSDT --trigger-value 5 --amount 100 --confirm --daemon

# 查看所有任务状态
bgtask list --json
```
