# 星云开放 API 文档

本文档描述星云智能客服机器人开放 API 的认证方式、核心接口、限流规则与错误码。

## 认证方式

所有接口使用 Bearer Token 认证。在控制台「API-KEY 管理」创建密钥后，放入请求头：

```http
Authorization: Bearer sk-xxxxxxxxxxxxxxxx
Content-Type: application/json
```

密钥仅显示一次，泄露后请立即在控制台吊销并重新生成。服务端校验失败返回 401，密钥权限不足返回 403。

## 对话接口

`POST /v1/chat/completions` —— 发起一轮对话。

请求体：

```json
{
  "session_id": "sess_1001",
  "query": "标准版支持私有化部署吗",
  "top_k": 5,
  "stream": false
}
```

`session_id` 用于串联多轮对话上下文，不传则服务端自动生成。返回体包含 `answer`、`references`（引用的知识片段与来源文档）与 `usage`（本轮消耗的 token）。

流式返回时设置 `"stream": true`，响应为 SSE，逐块返回 `delta` 文本。

## 知识库接口

- `POST /v1/knowledge/documents` —— 上传文档，支持 multipart 上传 PDF/Word/Markdown/HTML/TXT；
- `GET /v1/knowledge/documents/{doc_id}` —— 查询文档解析状态（`pending`/`parsing`/`ready`/`failed`）；
- `DELETE /v1/knowledge/documents/{doc_id}` —— 删除文档并同步移除其向量；
- `POST /v1/knowledge/search` —— 只检索不生成，用于调试召回效果，返回片段与相似度分数。

文档上传后需要等待解析与向量化，通常 10 万字文档约 2 分钟完成。

## 限流规则

| 版本 | QPS 上限 | 单请求最大 token | 并发对话数 |
|------|---------|----------------|-----------|
| 基础版 | 5 | 4096 | 5 |
| 标准版 | 20 | 8192 | 20 |
| 专业版 | 100 | 16384 | 100 |

超出限流返回 429，响应头 `Retry-After` 给出建议重试秒数。建议客户端实现指数退避重试。

## 错误码

| 错误码 | HTTP | 含义 | 处理建议 |
|--------|------|------|---------|
| `invalid_api_key` | 401 | 密钥无效或已吊销 | 重新生成密钥 |
| `permission_denied` | 403 | 无该资源权限 | 检查密钥绑定的知识库范围 |
| `doc_parse_failed` | 422 | 文档解析失败 | 检查文件是否加密或损坏 |
| `rate_limit_exceeded` | 429 | 触发限流 | 按 Retry-After 退避重试 |
| `knowledge_base_empty` | 409 | 知识库为空或全部未就绪 | 等待解析完成后再提问 |
| `internal_error` | 500 | 服务内部错误 | 携带 request_id 联系支持 |

## 接入示例

Python 调用示例：

```python
import requests

resp = requests.post(
    'https://api.nebula-ai.com/v1/chat/completions',
    headers={'Authorization': 'Bearer sk-xxx'},
    json={'session_id': 'sess_1001', 'query': '标准版多少钱'},
    timeout=30,
)
print(resp.json()['answer'], resp.json()['references'])
```

建议把 `references` 一并展示给最终用户，作为答案可溯源的依据。
