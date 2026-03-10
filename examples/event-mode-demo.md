# 事件模式示例

## 场景 1: 价格异动自动减仓（带风控）

"BTC 5 分钟内暴涨超 5%，自动减掉高杠杆仓位 30%，冷却 2 小时，放后台"

```bash
bgtask run event-mode \
  --symbol BTCUSDT \
  --event-type price_spike \
  --threshold 5 \
  --window 300 \
  --action reduce_position \
  --reduce-percent 30 \
  --position-filter high_leverage \
  --event-cooldown 7200 \
  --confirm \
  --daemon
```

每次减仓执行前会经过 6 步安全检查链（DANGER拦截 → dry-run → 日限 → 仓位比例 → 金额阈值 → 冲突检测）。

## 场景 2: 先 dry-run 测试事件检测

"先测一下 ETH 异动检测灵不灵，不要真执行"

```bash
bgtask run event-mode \
  --symbol ETHUSDT \
  --event-type price_spike \
  --threshold 3 \
  --action reduce_position \
  --reduce-percent 20 \
  --dry-run \
  --daemon
```

## 场景 3: 成交量突增监控

"监控 ETH 成交量，突增时提醒我"

```bash
bgtask run event-mode \
  --symbol ETHUSDT \
  --event-type volume_surge \
  --threshold 5 \
  --action alert_only \
  --daemon
```

## 场景 4: 紧急平仓（高危操作需 --confirm）

"BTC 异动超 8% 直接平仓"

```bash
bgtask run event-mode \
  --symbol BTCUSDT \
  --event-type price_spike \
  --threshold 8 \
  --action close_position \
  --confirm \
  --daemon
```

注意：close_position 是高危操作，**不加 `--confirm` CLI 会直接拒绝执行**。

## 场景 5: 资金费率异常

"资金费率异常时提醒"

```bash
bgtask run event-mode \
  --symbol BTCUSDT \
  --event-type funding_anomaly \
  --threshold 0.1 \
  --action alert_only \
  --daemon
```
