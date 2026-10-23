# 你好，我是 Alex 👋

后端工程师 / 公司技术负责人。做过实时数据链路、计费系统和两代产品的云原生基础设施，习惯从业务问题一路做到部署和运维。

## 精选项目

> 以下均为公司项目，代码未公开，只做脱敏描述。

### 云原生平台 · 从 0 到 1 与双云迁移

- 两代产品的基础设施均从零搭建：第一代在腾讯云 TKE，第二代迁到 GCP GKE，架构和运维体系保持连续。
- 作为公司技术负责人主导整体方案，并亲自落地架构、发布体系、身份与密钥、数据层连通、迁移割接和成本治理。
- GitOps：ArgoCD + Helm ApplicationSet 管理多服务、多环境；GitHub Actions 构建镜像并自动更新环境 tag。
- 身份与数据：GKE Workload Identity + 独立 GSA，CI 走 OIDC/WIF；Cloud SQL Auth Proxy + 共享 Cloud SQL/Redis，按服务做最小权限隔离。
- 迁移：双云并行、按服务割接，Kafka consumer group 隔离避免重复消费，保留回滚路径；旧云资源分批下线。
- 结果：环境可复现、发布自动化、权限收敛，固定成本下降。

### 实时喊单与排行榜

- 交易员的决策和喊单要实时推到前端，同时维护基金经理、分析师两套排行榜。
- 从 0 搭建 writer → Kafka → consumer → PostgreSQL/Redis → SSE 的链路。
- 关键设计：Kafka 削峰、消费幂等、Redis Pub/Sub 广播；SSE 用 afterSeq/afterTimestamp 支持断线续传；排行榜用 cache-aside + singleflight，全量缓存后内存排序。
- 结果：喊单广场和双榜查询稳定运行，事件可回放、消费可重试。

### Agent 可观测与 MCP 工具链

- 交易和研究 Agent 每天产生大量决策、订单、仓位日志，需要低成本查询和复盘。
- 搭建日志服务：冷数据写 BigQuery，热点决策索引写 PostgreSQL，提供跨 Agent 查询和订单/权益增量落账。
- 把决策查询从 BigQuery 全表扫改为 PG 索引表，消除超时；API Key 支持多 key 轮换。
- 封装 MCP Server，让管理员用自然语言复盘经营数据；并提供 Claude Code skills 包操作平台。

## 技术栈

- **主力**：Go（Gin / chi / Huma）、PostgreSQL、Redis、Kafka
- **常用**：MySQL、MongoDB、ClickHouse、BigQuery、Kubernetes、Terraform、ArgoCD、GCP / 腾讯云
- **了解**：TypeScript / React、Python

## 关注

- 实时数据链路与事件驱动架构
- 云原生、平台工程与成本治理
- AI Agent、MCP 与开发者工具

## 其他

- 接口契约用 Huma 声明请求/响应类型，自动生成 OpenAPI 3.1 和在线文档，减少文档与实现漂移。
- 做过支付回调、积分账务、过期扣减和运营后台。
