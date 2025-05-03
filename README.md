# OTTO-Mingbaiz
我的第一个github实战项目

## 数据集描述
本次竞赛的目标是预测电子商务中的点击量e-commerce clicks、加入购物车的行为cart additions以及订单数量orders。需要基于用户会话中的过往事件，构建一个多目标推荐系统。

训练数据包含完整的电子商务会话信息full e-commerce session information。对于测试数据中的每个会话，你的任务是预测在测试会话中最后一个时间戳 `ts` 之后出现的每种会话类型的 `aid` 值。换句话说，测试数据包含按时间戳截断的会话，我们需要预测截断点之后会发生什么。

文件说明：
- `train.jsonl` - 训练数据，包含完整的会话数据session data
    - `session` - 唯一的会话 ID  the unique session id
    - `events` - 会话中按时间排序的事件序列
        - `aid` - 相关事件的商品 ID（产品代码）the article id (product code) of the associated event
        - `ts` - 事件的 Unix 时间戳 the Unix timestamp of the event
        - `type` - 事件类型，即某个商品在会话期间是被点击了、被加入用户购物车了，还是被下单了
- `test.jsonl` - 测试数据，包含被截断的会话数据
    - 你的任务是预测会话截断后下一个被点击的 `aid`，以及其余被加入购物车和下单的 `aid`；对于每种会话类型，你最多可以预测 20 个值
- `sample_submission.csv` - 一个格式正确的提交示例文件 
/home/mingbai/Recommendation/OTTO/OTTO-Multi-Objective-Recommender-System

## 目标与评估

提交的内容根据每个动作的Recall@20进行评估，三个召回值是加权平均的：类型

$$ \text{分数} = 0.10 \cdot R_{\text{clicks}} + 0.30 \cdot R_{\text{carts}} + 0.60 \cdot R_{\text{orders}} $$

其中  $R$  定义为

 $R_{\text{type}} = \frac{\sum_{i}^{N} | \{\text{predicted aids}\}_{i,\text{type}} \cap \{\text{ground truth aids}\}_{i,\text{type}} |}{\sum_{i}^{N} \min (20, | \{\text{ground truth aids}\}_{i,\text{type}} |)} $

 $N$  是测试集中会话的总数，predicted aids是每个会话类型的预测（例如，提交文件中的每一行）在前20个预测后截断。

对于测试数据中的每个数据，我们的任务是预测测试会话最后一个时间戳之后发生的值。换句话说，测试数据包含按时间戳截断的会话，我们需要预测截断点之后发生的事情。

对于每个会话，只有一个真实的值，即会话期间点击的下一个值（尽管您仍然可以预测最多20个值）。真实的aid包含在会话期间添加到购物车和下订单的所有值。点击 援助 援助 购物车 订单 援助

每个组合应该在提交中单独一行出现，预测值应该用空格分隔。会话 类型 会话类型


rapid的安装
官方文档版本选择：https://docs.rapids.ai/install/#selector