# 个人投资分析助手配置说明

本说明用于把仓库收敛为“个人投资分析助手”用法，并演示如何把 `BR`（Broadridge Financial Solutions）加入自选股。

## 1. 运行时以哪个 `STOCK_LIST` 为准

项目支持多个配置来源，优先级从高到低通常为：

1. GitHub Actions `Variables` 中的 `STOCK_LIST`
2. GitHub Actions `Secrets` 中的 `STOCK_LIST`
3. 本地或服务器 `.env` 文件中的 `STOCK_LIST`
4. workflow / 代码中的默认回退值

这意味着：

- 如果仓库已经在 GitHub Actions 中配置了 `vars.STOCK_LIST` 或 `secrets.STOCK_LIST`，仅修改代码中的默认值不会改变实际运行结果。
- 如果你是本地运行或服务器运行，则应修改 `.env` 文件中的 `STOCK_LIST`。

## 2. 把 BR 加入自选股

### GitHub Actions 运行

进入：

`Settings -> Secrets and variables -> Actions`

优先检查 `Variables` 中是否存在 `STOCK_LIST`。

推荐示例：

```env
STOCK_LIST=600519,BR
```

如果你希望保留原来的 A 股，再加入 BR：

```env
STOCK_LIST=600519,300750,002594,BR
```

### 本地 / 服务器运行

在 `.env` 中设置：

```env
STOCK_LIST=600519,300750,002594,BR
```

## 3. BR 属于什么股票

- `BR` 是美股代码
- 公司名称：`Broadridge Financial Solutions`
- 关注这类标的时，建议把市场复盘区域调整为 `us` 或 `both`

例如：

```env
MARKET_REVIEW_REGION=both
```

或仅做美股：

```env
MARKET_REVIEW_REGION=us
```

## 4. 个人投资助手推荐配置

```env
STOCK_LIST=600519,300750,002594,BR
MARKET_REVIEW_ENABLED=true
MARKET_REVIEW_REGION=both
REPORT_TYPE=simple
SINGLE_STOCK_NOTIFY=false
BACKTEST_ENABLED=true
AGENT_MODE=true
```

## 5. 当前仓库中已做的默认改动

当前 workflow 默认回退值已补入 `BR`，示例为：

```env
STOCK_LIST=600519,BR
```

但再次强调：

**如果仓库已有 GitHub Variables / Secrets 中的 `STOCK_LIST`，则运行时仍以那里的值为准。**
