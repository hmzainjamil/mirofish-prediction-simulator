# MiroFish Prediction Simulator

MiroFish 是一个网页应用，可根据输入材料构建多 Agent 模拟环境、运行情景模拟并生成报告。模型生成的模拟结果属于情景分析，不是经过验证的现实预测。

> **状态：** 本次检查了源代码目录结构；没有验证实际运行、外部服务、部署、模拟质量或测试结果。

## 代码结构

| 部分 | 路径 | 证据 |
|---|---|---|
| Vue 3 和 Vite 前端 | frontend/ | 源码和 package scripts |
| Flask API | backend/app/api/ | 图谱、模拟和报告路由模块 |
| 模拟与图谱服务 | backend/app/services/ | 图谱构建、角色生成、模拟和报告源码 |
| 外部服务 | Zep Cloud 和兼容 OpenAI API 的 LLM 服务 | 依赖与配置引用；本次未连接验证 |
| 研究与评估 | backend/scripts/ | 包含角色格式脚本；不宣称测试已通过 |

后端依赖中包含 OASIS/Camel 社交模拟库，并引用 Zep Cloud 图谱记忆。服务兼容性取决于外部服务版本和配置。

## 本地开发

需要 Python 3.11 或更高版本、Node.js/npm 和 uv。

    cp .env.example .env
    # 在 .env 中设置所需的 LLM 和 Zep 配置
    npm run setup:all
    npm run dev

命令依据根目录 package scripts 和后端配置整理，本次未执行。前端使用 3000 端口，并将 API 请求代理到 5001 端口。后端默认监听 0.0.0.0:5001，前端开发脚本也使用 Vite 的 --host。这两个服务可能被网络访问。请勿暴露在不可信网络中；共享或公开使用前应审查并限制监听地址。

## 配置与数据

根目录 .env.example 列出了 LLM_API_KEY、LLM_BASE_URL、LLM_MODEL_NAME、ZEP_API_KEY 和可选服务商设置。请把凭证放在未跟踪的本地 .env 文件中。

输入材料、提示词、生成的 Agent 内容和报告可能被发送到所配置的 LLM 与 Zep 服务。本仓库未证明数据仅在本地处理，也未验证第三方的数据保留政策。处理敏感材料前，请先检查服务商条款和数据控制选项。

## 验证与部署

旧版 README 列出的单元、集成、Playwright、冒烟测试、覆盖率、耗时和 CI 计划，在检查的源码目录中没有找到对应依据。相关内容已移除，等待可复现证据。根目录 package 当前提供安装、开发和前端构建脚本，没有声明通用测试脚本。

仓库中的 Docker Compose 使用 ghcr.io/666ghj/mirofish:latest 镜像，并不会构建当前检出的源码。不要假设该镜像与此仓库版本一致。

## 限制

- 模拟适用于探索情景，不证明预测准确性，也不能证明未来事件会如何发展。
- 结果质量受输入材料、模型/服务商行为、模拟设置和假设影响。
- 本说明不声明基准测试结果、生产部署、安全审查或预测准确性证据。

## 文档

- [文档索引](docs/README.md)
- [后端 API 模块](backend/app/api/)
- [模拟服务](backend/app/services/)
- [后端配置](backend/app/config.py)
- [环境变量模板](.env.example)
- [许可证](LICENSE)

## 许可证

根目录 [LICENSE](LICENSE) 为 GNU Affero General Public License 第 3 版。使用和分发请阅读许可证全文。