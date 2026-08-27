1、phyton
2、模型调用
3、react，function call
4、hello agent
learn-claude-code
learn-harness-engineering
craft-agents-oss
zread项目解析 
5.how claude code works
6、rag
7、langchain、langgraph







## **stage0:**

​	我的场景为什么需要 agent，而不是普通 workflow？

​	1、**workflow**是预定义的、确定性的任务编排流程，是DAG有向无环图，而**agent**是具备感知、规划、行动能力的自主实体、能以目标为导向动态决策，是一个循环LOOP，核心是planning+tool use，引入了不确定性，需要关注eval和safety

ReAct论文

## stage1

​	safety：

| 护栏           | 实现方式                             | 防御场景                                 | 研究生思考                                             |
| -------------- | ------------------------------------ | ---------------------------------------- | ------------------------------------------------------ |
| max_steps      | `for step in range(max_steps)`       | 模型陷入循环：反复调同一工具、推理死循环 | 最优值如何确定？能否让模型自己判断"我还需要几步"？     |
| timeout        | `time.time() - start_time > timeout` | 网络卡死、模型响应极慢、工具执行阻塞     | 单步超时 vs 总超时，哪个更合理？能否做渐进式 timeout？ |
| error_handling | `try-except` 包裹 API 调用和工具执行 | API 限流(429)、工具崩溃、JSON 解析失败   | 错误信息是否应该喂回模型让它自我修正？还是直接终止？   |