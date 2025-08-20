---
description: ZenML 中文介绍 - 统一的机器学习运维（MLOps）框架
icon: lightbulb
---

# ZenML 中文介绍

<div align="center">
  <h1>面向可靠AI的MLOps - 从经典机器学习到智能代理</h1>
  <h3>统一的工具包，用于部署从决策树到复杂AI代理的一切，建立在您已经信任的MLOps原则之上。</h3>
</div>

## 🌟 ZenML 是什么？

**ZenML** 是一个可扩展的开源 MLOps 框架，用于创建可移植、生产就绪的 **机器学习管道**。它专为数据科学家、机器学习工程师和 MLOps 开发人员设计，帮助他们从开发到生产的整个过程中进行协作。

### 核心优势

- **🔄 统一框架**：一个平台管理经典机器学习模型和现代AI代理
- **🚀 生产就绪**：内置版本控制、监控和部署能力
- **🔌 丰富集成**：支持 MLflow、LangChain、LlamaIndex 等流行工具
- **📊 可视化界面**：直观的仪表板查看管道执行和结果
- **🛠️ 灵活配置**：可配置的技术栈组件

## 🎯 解决的问题

### 传统MLOps的挑战

在现代AI时代，机器学习工程师面临着新的挑战：

- **适应困难**：传统的MLOps实践（严格测试、版本控制、CI/CD）无法直接应用于代理开发
- **技术栈分离**：团队为LLM系统构建独立的技术栈，导致维护复杂性倍增
- **反馈循环中断**：从本地环境到生产部署的周期过长，难以及时获得性能反馈

### ZenML的解决方案

ZenML 提供统一的MLOps框架，将久经考验的机器学习原则扩展到AI代理的新世界：

```python
# 上午：您的sklearn管道仍然版本化且可重现
train_and_deploy_classifier()

# 下午：您的新代理评估管道使用相同的逻辑
evaluate_and_deploy_agent()

# 同一平台，同样的原则，新的可能性
```

## 🏗️ 核心概念

### 1. 步骤（Steps）

步骤是使用 `@step` 装饰器注释的函数，是ZenML中的基本构建块：

```python
from zenml import step

@step
def data_loader() -> pd.DataFrame:
    """加载训练数据"""
    return pd.read_csv("data.csv")

@step
def model_trainer(data: pd.DataFrame) -> sklearn.base.BaseEstimator:
    """训练机器学习模型"""
    model = RandomForestClassifier()
    X, y = data.drop('target', axis=1), data['target']
    model.fit(X, y)
    return model
```

### 2. 管道（Pipelines）

管道将多个步骤组织成有序的工作流：

```python
from zenml import pipeline

@pipeline
def training_pipeline():
    """完整的训练管道"""
    data = data_loader()
    model = model_trainer(data)
    return model

# 执行管道
training_pipeline()
```

### 3. 技术栈（Stacks）

技术栈定义了管道执行时使用的基础设施和工具：

- **编排器（Orchestrator）**：管理管道执行（如 Kubernetes、Airflow）
- **工件存储（Artifact Store）**：存储管道输出（如 S3、GCS）
- **容器注册表（Container Registry）**：存储Docker镜像
- **实验跟踪器（Experiment Tracker）**：记录实验结果（如 MLflow、Weights & Biases）

## 🚀 快速开始

### 安装

```bash
# 安装ZenML核心包
pip install zenml

# 安装流行的集成
zenml integration install langchain llamaindex mlflow
```

### 初始化项目

```bash
# 初始化ZenML项目
zenml init

# 使用模板快速开始
zenml init --template agent-evaluation-starter
```

### 第一个AI管道

```python
# my_first_agent_pipeline.py
from zenml import pipeline, step
import pandas as pd

@step
def load_test_queries() -> list[str]:
    """加载测试查询"""
    return [
        "如何退货？",
        "你们的退款政策是什么？",
        "我可以更改我的订单吗？"
    ]

@step
def run_customer_service_agent(queries: list[str]) -> list[str]:
    """运行客服代理"""
    # 使用任何框架 - LangGraph、CrewAI、原生OpenAI
    agent = YourExistingAgent()
    
    # 自动版本控制提示词、工具、代码和配置
    return [agent.run(q) for q in queries]

@step
def evaluate_responses(queries: list[str], responses: list[str]) -> dict:
    """评估响应质量"""
    quality = llm_judge(queries, responses)
    latency = measure_response_times()
    costs = calculate_token_usage()
    
    return {
        "quality": quality.mean(),
        "p95_latency": latency.quantile(0.95),
        "cost_per_query": costs.mean()
    }

@pipeline
def customer_service_evaluation_pipeline():
    """客服代理评估管道"""
    queries = load_test_queries()
    responses = run_customer_service_agent(queries)
    metrics = evaluate_responses(queries, responses)
    
    # 指标自动记录、版本化并可在仪表板中比较
    return metrics

if __name__ == "__main__":
    customer_service_evaluation_pipeline()
    print("查看您的仪表板：http://localhost:8080")
```

## 📊 仪表板功能

ZenML提供强大的Web仪表板，包括：

### 开源版本功能
- **管道可视化**：DAG形式展示管道结构和执行状态
- **工件可视化**：查看和下载管道产生的数据和模型
- **执行历史**：跟踪所有管道运行记录
- **技术栈管理**：可视化配置和管理组件
- **集成特定可视化**：支持各种ML工具的专门可视化

### ZenML Pro 功能
- **模型控制平面**：高级ML资产跟踪和管理
- **实验比较工具**：并排比较不同实验结果
- **基于角色的访问控制**：企业级用户和权限管理
- **团队管理**：组织和团队结构支持

## 🔗 集成生态系统

ZenML支持丰富的第三方工具集成：

### 实验跟踪
- **MLflow**：实验跟踪和模型注册
- **Weights & Biases**：实验管理和可视化
- **Neptune**：元数据存储和实验比较

### 编排工具
- **Airflow**：工作流编排
- **Kubeflow**：Kubernetes原生ML工作流
- **Kubernetes**：容器编排

### 云服务
- **AWS**：SageMaker、S3、ECR
- **Google Cloud**：Vertex AI、GCS、GCR
- **Azure**：Azure ML、Blob Storage

### AI/LLM 框架
- **LangChain**：LLM应用开发框架
- **LlamaIndex**：数据框架用于LLM应用
- **OpenAI**：GPT模型API
- **HuggingFace**：开源模型和数据集

## 💡 使用场景

### 1. 经典机器学习
```python
@pipeline
def classical_ml_pipeline():
    """传统机器学习管道"""
    data = load_data()
    processed_data = preprocess_data(data)
    model = train_model(processed_data)
    metrics = evaluate_model(model, processed_data)
    deploy_model(model)
    return metrics
```

### 2. LLM微调和部署
```python
@pipeline
def llm_fine_tuning_pipeline():
    """LLM微调管道"""
    dataset = prepare_training_data()
    model = fine_tune_llm(dataset, base_model="llama-2-7b")
    evaluation_results = evaluate_llm(model)
    deploy_llm(model)
    return evaluation_results
```

### 3. AI代理评估
```python
@pipeline
def agent_comparison_pipeline():
    """多代理架构比较"""
    test_data = load_production_samples()
    
    # 测试不同的代理架构
    single_agent_results = test_single_agent(test_data)
    multi_agent_results = test_multi_agent(test_data)
    hierarchical_results = test_hierarchical_agents(test_data)
    
    # 比较性能
    comparison = compare_architectures(
        single_agent_results,
        multi_agent_results, 
        hierarchical_results
    )
    
    return comparison
```

## 🛠️ 高级功能

### 缓存机制
ZenML提供智能缓存，避免重复计算：

```python
@step(enable_cache=True)
def expensive_computation(data: pd.DataFrame) -> pd.DataFrame:
    """耗时的数据处理步骤"""
    # 这个步骤的结果会被缓存
    # 如果输入数据没有变化，将直接使用缓存结果
    return process_large_dataset(data)
```

### 条件执行
根据条件决定管道执行路径：

```python
@pipeline
def conditional_pipeline():
    """条件执行管道"""
    data = load_data()
    
    if data.shape[0] > 10000:
        # 大数据集使用分布式处理
        processed = distributed_preprocessing(data)
    else:
        # 小数据集使用单机处理
        processed = local_preprocessing(data)
    
    model = train_model(processed)
    return model
```

### 参数化管道
使用参数使管道更加灵活：

```python
@pipeline
def parameterized_pipeline(
    model_type: str = "random_forest",
    test_size: float = 0.2
):
    """参数化的训练管道"""
    data = load_data()
    train_data, test_data = split_data(data, test_size=test_size)
    
    if model_type == "random_forest":
        model = train_rf_model(train_data)
    elif model_type == "svm":
        model = train_svm_model(train_data)
    else:
        model = train_neural_network(train_data)
    
    metrics = evaluate_model(model, test_data)
    return model, metrics

# 使用不同参数运行
parameterized_pipeline(model_type="svm", test_size=0.3)
```

## 📈 最佳实践

### 1. 代码组织
- 将步骤放在单独的模块中以便重用
- 使用清晰的命名约定
- 为所有步骤添加文档字符串

### 2. 数据管理
- 使用类型注解确保数据一致性
- 实施数据验证步骤
- 使用ZenML的工件存储管理数据版本

### 3. 实验跟踪
- 记录所有重要的超参数和指标
- 使用标签组织相关实验
- 定期清理过时的实验数据

### 4. 部署策略
- 使用不同的技术栈配置区分开发、测试和生产环境
- 实施自动化测试验证部署的模型
- 监控生产模型的性能和漂移

## 🎓 学习资源

### 官方文档
- **[入门指南](https://docs.zenml.io/user-guides/starter-guide)**：30分钟从零到生产
- **[LLMOps指南](https://docs.zenml.io/user-guides/llmops-guide)**：LLM应用的特定模式
- **[SDK参考](https://sdkdocs.zenml.io/)**：完整的API文档

### 视频教程
- **[11分钟介绍视频](https://www.youtube.com/watch?v=wEVwIkDvUPs)**：快速了解ZenML核心概念

### 示例项目
浏览 `examples/` 目录查看完整的项目示例：
- **端到端NLP项目**：完整的自然语言处理工作流
- **代理评估**：AI代理性能评估管道
- **模型部署**：生产级模型部署示例

## 🤝 社区和支持

### 开源社区
- **GitHub**：[zenml-io/zenml](https://github.com/zenml-io/zenml) - 提交问题和贡献代码
- **Slack社区**：加入ZenML用户和开发者社区
- **论坛**：获取帮助和分享最佳实践

### 商业支持
- **ZenML Pro**：企业级功能和专业支持
- **咨询服务**：MLOps实施和优化咨询
- **培训课程**：团队培训和最佳实践指导

## 🆚 常见问题

**问：我需要重写现有的代理或模型代码才能使用ZenML吗？**
答：不需要。只需用 `@step` 装饰器包装您现有的代码。继续使用 `scikit-learn`、PyTorch、LangGraph、LlamaIndex 或原生API调用。ZenML 编排您的工具，而不是替换它们。

**问：这与 LangSmith/Langfuse 有什么不同？**
答：它们为LLM应用提供优秀的可观测性。我们编排**整个AI技术栈的完整MLOps生命周期**。使用ZenML，您可以在一个统一框架中管理经典ML模型和AI代理，从开发和评估一直到生产部署。

**问：我可以使用现有的MLflow/W&B设置吗？**
答：可以！我们与两者都集成。您的实验，我们的管道。

**问：这只是带有额外步骤的MLflow吗？**
答：不是。MLflow跟踪实验。我们编排整个开发过程 - 从训练和评估到部署和监控 - 适用于模型和代理。

**问：成本如何？我负担不起另一个平台。**
答：ZenML的开源版本永久免费。您可能已经拥有所需的基础设施（如Kubernetes集群和对象存储）。我们只是帮助您更好地将其用于MLOps。

## 📜 许可证

ZenML在Apache License Version 2.0条款下分发。详情请参见[LICENSE](https://github.com/zenml-io/zenml/blob/main/LICENSE)。

---

*立即开始您的ZenML之旅，将您的AI工作流从实验带到生产！*