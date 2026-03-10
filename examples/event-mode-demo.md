# 事件模式示例

## 场景 1: 价格异动减仓

"BTC 异动超 3% 时，高杠杆仓位自动减仓 20%"

```bash
bgtask run event-mode \
  --symbol BTCUSDT \
  --event-type price_spike \
  --threshold 3 \
  --action reduce_position \
  --reduce-percent 20 \
  --position-filter high_leverage \
  --daemon
```

## 场景 2: 成交量突增监控

"监控 ETH 成交量，突增时提醒我"

```bash
bgtask run event-mode \
  --symbol ETHUSDT \
  --event-type volume_surge \
  --threshold 5 \
  --action alert_only \
  --daemon
```

## 场景 3: 资金费率异常

"资金费率异常时提醒"

```bash
bgtask run event-mode \
  --symbol BTCUSDT \
  --event-type funding_anomaly \
  --threshold 0.1 \
  --action alert_only \
  --daemon
```
