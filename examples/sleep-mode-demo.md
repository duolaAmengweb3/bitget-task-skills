# 睡觉模式示例

## 场景 1: 夜间抄底

"今晚帮我盯着 BTC，如果跌超 2.5% 就买入 100U，稳健档"

解析结果：
```bash
bgtask run sleep-mode \
  --symbol BTCUSDT \
  --trigger-type price_drop \
  --trigger-value 2.5 \
  --action buy \
  --amount 100 \
  --risk-profile conservative \
  --max-triggers 1 \
  --duration 28800 \
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
