# 知识库建设规范 + 文档模板

## 知识库建设规范
1. 知识库不能建立目录区分错误还是流程问题，只能通过文件名，如
| 类型前缀    | 含义           |
| ------- | ------------ |
| `ERR`   | 报错 / 异常      |
| `PROC`  | 流程 / 操作指引    |
| `GUIDE` | 规则 / 边界 / 说明 |
| `FAQ`   | 高频问答         |

2. Coze 的 RAG（知识库） 很吃结构，结构化文档 > 杂乱文档


3. 知识库（RAG）
支持上传：

PDF / Word / TXT

FAQ 文档

自动向量化

对话中按需召回

支持「基于知识库回答

4. 把日常遇到的问题或者流程，按结构输出文档，然后上传到知识库
【错误现象】
【涉及模块】
【常见原因】
【排查步骤】
【是否可自行处理】
【何时必须升级 IT】

5. 上传完成进行提问测试，多种提问方式看看是否可以命中

用真实问题测试 Bot：

是否能准确命中

是否能合理追问

是否不会“下结论”

6. 文件名 = 检索命中率的核心，一定要包含：关键词 + 现象。如
ERR_WMS_ORDER_01_订单导入成功但不下发任务.md
ERR_WMS_<模块>_<序号>_<用户能看懂的现象>.md

7. 每篇一个 .md 文件

按目录分批上传

不要一次性混传 PDF + Word

不推荐

一个文档写多个报错

大而全的操作手册直接丢进去

图片型 PDF（检索命中率差）



## 文档模板

【常见问法触发】

- WISE 怎么查日志？

- API 订单有没有到 WISE？

- Shopify 订单在哪里查日志？

- DI 订单怎么查日志？

- 接口发了但系统没记录，怎么排查？

- 怎么确认订单有没有到 WISE？


---


【流程名称】

WISE 日志查询（API / Shopify / DI）


【适用场景】

当接口订单、Shopify 订单或 DI 数据在 WMS / WISE 中表现异常，

需要确认请求是否到达 WISE、是否被系统正确接收和处理时，

可通过 WISE 日志进行排查。


【适用问题示例】

- 接口文件已发送，但 WMS 中无任何记录

- Shopify 订单未生成 WMS 订单

- DI 数据未生效或状态异常

- 需要确认某个订单是否到达 WISE


【涉及系统】

- WISE

- Public API

- Shopify

- DI（Data Integration）


---


【操作流程】


### 第 1 步：登录 WISE 系统

使用个人账号登录 WISE 系统。


> 操作要点： 

> 确保使用有权限的账号登录。


---


### 第 2 步：进入 Admin 模块并选择仓库

在 WISE 页面中：

- Modules 选择 **Admin**

- Facility 选择 **对应仓库**


> 说明： 


> Facility 必须与订单所属仓库一致，否则可能查不到日志。


![WISE 中选择 Modules 为 Admin 并选择 Facility](https://raw.githubusercontent.com/wulinggang8-sudo/coze-kb-assets/main/wise2/logs/WISE%20%E4%B8%AD%E9%80%89%E6%8B%A9%20Modules%20%E4%B8%BA%20Admin%20%E5%B9%B6%E9%80%89%E6%8B%A9%20Facility.png)


### 第 3 步：进入日志查询目录

按以下路径进入日志页面：


**Service → Logs → Public API Order**


> 说明： 

> - 该目录用于查询 API / Shopify / DI 相关订单日志 

> - 若需查询其他类型日志，应选择对应的日志目录


![进入日志查询目录](https://raw.githubusercontent.com/wulinggang8-sudo/coze-kb-assets/main/wise2/logs/%E8%BF%9B%E5%85%A5%E6%97%A5%E5%BF%97%E6%9F%A5%E8%AF%A2%E7%9B%AE%E5%BD%95.png) 

### 第 4 步：填写查询条件

在日志查询页面中，填写以下信息：

- 客户（Customer）

- 仓库（Facility）

- 订单号（Order Number）


> 操作要点： 


> - 订单号需与上游系统发送的一致 

> - 仓库选择错误将导致查询无结果


![填充对应的客户&仓库和订单号](https://raw.githubusercontent.com/wulinggang8-sudo/coze-kb-assets/main/wise2/logs/%E5%A1%AB%E5%85%85%E5%AF%B9%E5%BA%94%E7%9A%84%E5%AE%A2%E6%88%B7%26%E4%BB%93%E5%BA%93%E5%92%8C%E8%AE%A2%E5%8D%95%E5%8F%B7.png)


### 第 5 步：查询并查看日志结果

执行查询后，查看是否存在对应订单的日志记录，

并关注请求状态及返回信息。


---


【查询结果解读】

- **查询到日志**

 - 说明请求已到达 WISE

 - 可根据日志内容判断接口处理结果

- **未查询到日志**

 - 请求可能未到达 WISE

 - 需向上游系统或接口方确认发送情况


---


【关键注意事项】

- 必须选择正确的 Facility（仓库）

- 订单号需准确无误

- 不同接口类型日志路径可能不同


【是否可自行处理】

- 是 

- OPS / BA 可自行完成日志查询和基础判断


【何时必须升级 IT】

- 查询到日志但返回异常或报错

- 日志显示系统错误或处理失败

- 多次查询均无日志且需要进一步接口排查
