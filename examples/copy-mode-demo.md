# 复制模式示例

## 场景 1: 筛选低回撤交易员（dry-run）

"帮我筛 30 天低回撤的交易员，预算 500U"

```bash
bgtask run copy-mode \
  --sort-by roi_drawdown_ratio \
  --period 30d \
  --min-winrate 60 \
  --max-drawdown 20 \
  --budget 500 \
  --max-per-trader 200 \
  --allocation balanced
```

## 场景 2: 自动执行跟单

确认推荐结果后：

```bash
bgtask run copy-mode \
  --sort-by roi_drawdown_ratio \
  --period 30d \
  --min-winrate 60 \
  --max-drawdown 20 \
  --budget 500 \
  --auto-execute
```

## 场景 3: 高胜率优先

"找胜率最高的交易员，预算 1000U，均分"

```bash
bgtask run copy-mode \
  --sort-by winrate \
  --min-winrate 70 \
  --budget 1000 \
  --allocation equal
```
