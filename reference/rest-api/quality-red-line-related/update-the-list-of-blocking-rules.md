# 更新拦截规则列表

### 请求方法/请求路径

#### PUT  /ms/openapi/api/apigw/v3/projects/{projectId}/quality/rules/{ruleHashId}/update

### 资源描述

#### 更新拦截规则列表

### 输入参数说明

#### Body参数

| 参数名称 | 参数类型 | 必须 | 参数说明 | 默认值 |
| :--- | :--- | :--- | :--- | :--- |
| body | [规则更新请求](update-the-list-of-blocking-rules.md) | 是 | 规则内容 |  |

#### Path参数

| 参数名称 | 参数类型 | 必须 | 参数说明 | 默认值 |
| :--- | :--- | :--- | :--- | :--- |
| projectId | string | 是 | 项目ID |  |
| ruleHashId | string | 是 | 规则ID |  |

#### 响应

| HTTP代码 | 说明 | 参数类型 |
| :--- | :--- | :--- |
| 200 | successful operation | [数据返回包装模型Boolean](update-the-list-of-blocking-rules.md) |

#### 请求样例

```javascript
curl -X PUT '[请替换为API地址栏请求地址]'
```

#### HEADER样例

```javascript
accept: application/json
Content-Type: application/json
```

### 返回样例-200

```javascript
{
  "data" : true,
  "message" : "String",
  "status" : 0
}
```

## 规则更新请求

| 参数名称 | 参数类型 | 必须 | 参数说明 |
| :--- | :--- | :--- | :--- |
| templateRange | List | 是 | 生效的流水线模板id集合 |
| auditUserList | List | 否 | 审核通知人员 |
| range | List | 是 | 生效的流水线id集合 |
| auditTimeoutMinutes | integer | 否 | 审核超时时间 |
| notifyTypeList | List | 否 | 通知类型 |
| notifyUserList | List | 否 | 通知人员名单 |
| controlPointPosition | string | 是 | 控制点位置 |
| name | string | 是 | 规则名称 |
| notifyGroupList | List | 否 | 通知组名单 |
| operation | ENUM\(END, AUDIT, \) | 是 | 操作类型 |
| indicatorIds | List&lt;[CreateRequestIndicator](update-the-list-of-blocking-rules.md)&gt; | 是 | 指标类型 |
| controlPoint | string | 是 | 控制点 |
| gatewayId | string | 否 | 红线匹配的id |
| desc | string | 是 | 规则描述 |

## CreateRequestIndicator

| 参数名称 | 参数类型 | 必须 | 参数说明 |
| :--- | :--- | :--- | :--- |
| threshold | string | 否 | threshold |
| hashId | string | 否 | hashId |
| operation | string | 否 | operation |

## 数据返回包装模型Boolean

| 参数名称 | 参数类型 | 必须 | 参数说明 |
| :--- | :--- | :--- | :--- |
| data | boolean | 否 | 数据 |
| message | string | 否 | 错误信息 |
| status | integer | 是 | 状态码 |

