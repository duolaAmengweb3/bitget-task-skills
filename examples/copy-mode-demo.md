# 复制模式示例

## 场景 1: 量化筛选交易员（dry-run）

"帮我做一次量化筛选：30 天胜率 65% 以上、回撤不超 15%，按收益回撤比排序，预算 1000U，均衡分配，先看报告"

```bash
bgtask run copy-mode \
  --sort-by roi_drawdown_ratio \
  --period 30d \
  --min-winrate 65 \
  --max-drawdown 15 \
  --budget 1000 \
  --max-per-trader 300 \
  --allocation balanced
```

输出量化分析报告：每个交易员的 ROI、胜率、最大回撤、综合评分，以及预算分配方案。

## 场景 2: 确认后自动执行跟单

确认推荐结果后：

```bash
bgtask run copy-mode \
  --sort-by roi_drawdown_ratio \
  --period 30d \
  --min-winrate 65 \
  --max-drawdown 15 \
  --budget 1000 \
  --max-per-trader 300 \
  --allocation balanced \
  --auto-execute
```

每笔跟单执行前会经过安全检查链，交易计数仅在成功后递增。

## 场景 3: 高胜率优先 + 均分

"找胜率最高的交易员，预算 1000U，均分"

```bash
bgtask run copy-mode \
  --sort-by winrate \
  --min-winrate 70 \
  --budget 1000 \
  --allocation equal
```

## 场景 4: 加权分配集中优质交易员

"预算 2000U，按评分加权分配，集中资金到最优交易员"

```bash
bgtask run copy-mode \
  --sort-by roi_drawdown_ratio \
  --period 30d \
  --min-winrate 60 \
  --max-drawdown 20 \
  --budget 2000 \
  --max-per-trader 500 \
  --allocation weighted
```

加权模式按评分比例分配，高评分交易员获得更多预算，单人上限 500U。
