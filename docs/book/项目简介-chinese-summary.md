---
description: ZenML项目简介 - 统一MLOps框架概述
icon: info
---

# ZenML 项目简介

## 🎯 什么是ZenML？

ZenML是一个**开源MLOps框架**，专为构建生产就绪的机器学习管道而设计。它统一了从传统机器学习到现代AI智能体的整个开发流程。

## 🔑 核心价值

### 统一技术栈
- **一个框架**：同时支持经典ML模型和AI智能体
- **一致体验**：相同的开发模式和部署流程
- **无缝迁移**：从本地开发到云端生产

### 生产就绪
- **可追溯性**：完整的数据和模型血缘关系
- **可重现性**：版本化的管道和制品
- **可扩展性**：支持云端大规模部署

## 🏗️ 核心概念

| 概念 | 说明 | 示例 |
|------|------|------|
| **步骤 (Step)** | 执行特定任务的函数 | 数据加载、模型训练、评估 |
| **管道 (Pipeline)** | 步骤的有序组合 | 训练管道、推理管道 |
| **技术栈 (Stack)** | 基础设施配置 | 本地栈、云端栈 |
| **制品 (Artifact)** | 步骤的输出结果 | 数据集、模型、指标 |

## 💻 快速示例

```python
from zenml import step, pipeline

@step
def load_data() -> pd.DataFrame:
    """加载数据"""
    return pd.read_csv("data.csv")

@step
def train_model(data: pd.DataFrame) -> sklearn.BaseEstimator:
    """训练模型"""
    model = RandomForestClassifier()
    return model.fit(data)

@pipeline
def ml_pipeline():
    """机器学习管道"""
    data = load_data()
    model = train_model(data)
    return model

# 运行管道
if __name__ == "__main__":
    ml_pipeline()
```

## 🚀 主要特性

### 📊 多样化支持
- **传统ML**：scikit-learn、PyTorch、TensorFlow
- **LLM应用**：LangChain、LlamaIndex、OpenAI
- **AI智能体**：CrewAI、LangGraph、AutoGen

### 🔧 丰富集成
- **编排器**：Kubernetes、Airflow、Kubeflow
- **云平台**：AWS、GCP、Azure
- **监控**：MLflow、W&B、Neptune

### 🎛️ 企业功能
- **权限控制**：基于角色的访问管理
- **安全认证**：服务连接器
- **模型管理**：版本化的模型注册表

## 📈 适用场景

### 🎯 经典ML项目
- 批量预测管道
- 模型训练和评估
- 超参数优化
- A/B测试框架

### 🤖 AI智能体项目
- 多智能体系统
- RAG应用构建
- LLM微调管道
- 智能体性能评估

### 🏭 生产环境
- 持续训练(CT)
- 持续部署(CD)
- 模型监控
- 数据漂移检测

## 🏁 快速开始

### 1. 安装
```bash
pip install zenml
zenml integration install sklearn  # 安装所需集成
```

### 2. 初始化
```bash
zenml init                        # 初始化项目
zenml init --template starter     # 使用模板
```

### 3. 启动UI
```bash
zenml login --local               # 启动本地界面
# 访问 http://localhost:8080
```

### 4. 运行示例
```bash
python run.py                     # 运行示例管道
```

## 📚 学习路径

### 🏃‍♂️ 快速入门 (30分钟)
1. [安装指南](https://docs.zenml.io/getting-started/installation)
2. [Hello World](https://docs.zenml.io/getting-started/hello-world)
3. [核心概念](https://docs.zenml.io/getting-started/core-concepts)

### 📖 深度学习 (2-4小时)
1. [入门指南](https://docs.zenml.io/user-guides/starter-guide)
2. [生产指南](https://docs.zenml.io/user-guides/production-guide)
3. [LLMOps指南](https://docs.zenml.io/user-guides/llmops-guide)

### 🛠️ 实践项目 (1-2天)
1. [端到端示例](https://github.com/zenml-io/zenml/tree/main/examples/e2e)
2. [LLM RAG项目](https://github.com/zenml-io/zenml-projects/tree/main/llm-complete-guide)
3. [智能体工作流](https://github.com/zenml-io/zenml-projects/tree/main/deep_research)

## 🌍 社区资源

- **GitHub**: [zenml-io/zenml](https://github.com/zenml-io/zenml)
- **文档**: [docs.zenml.io](https://docs.zenml.io)
- **博客**: [zenml.io/blog](https://zenml.io/blog)
- **Discord**: [社区讨论](https://zenml.io/slack-invite/)

## 📄 开源协议

Apache License 2.0 - 详见 [LICENSE](https://github.com/zenml-io/zenml/blob/main/LICENSE)

---

**开始您的ZenML之旅！** 从简单的ML管道到复杂的AI智能体系统，ZenML为您提供统一、可靠的MLOps解决方案。