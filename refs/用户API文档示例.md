
# 用户管理API

## 概述

用户管理API提供了创建、查询、更新和删除用户的功能。所有端点都需要有效的API密钥进行认证。

## 认证

所有API请求都需要在HTTP头中包含`X-API-Key`字段：

```http
X-API-Key: your_api_key_here
```

## 端点

### 创建用户

创建一个新用户。

#### 请求

```javascript
POST /api/v1/users
Content-Type: application/json
X-API-Key: your_api_key_here

{
  "username": "johndoe",
  "email": "john.doe@example.com",
  "role": "user"
}
```

#### 参数

| 名称 | 类型 | 必填 | 描述 |
|-----|-----|-----|-----|
| username | string | 是 | 用户名，3-20个字符，只能包含字母、数字和下划线 |
| email | string | 是 | 有效的电子邮件地址 |
| role | string | 否 | 用户角色，可选值：admin、user、guest，默认为user |

#### 响应

```javascript
Status: 201 Created
Content-Type: application/json

{
  "id": "usr_123456",
  "username": "johndoe",
  "email": "john.doe@example.com",
  "role": "user",
  "created_at": "2025-06-07T10:30:00Z"
}
```

#### 错误码

| 状态码 | 描述 | 可能原因 |
|-----|-----|-----|
| 400 | 请求无效 |参数格式错误或缺失必填字段|
| 409 | 冲突 | 用户名或邮箱已存在|
| 429 | 请求过多 | 超出API调用限制|

```javascript
import requests
import json

def create_user(api_key, username, email, role="user"):
    """
    创建新用户
    
    参数:
        api_key (str): API密钥
        username (str): 用户名
        email (str): 电子邮件
        role (str, 可选): 用户角色，默认为"user"
        
    返回:
        dict: 创建的用户信息
    """
    url = "https://api.example.com/api/v1/users"
    headers = {
        "Content-Type": "application/json",
        "X-API-Key": api_key
    }
    payload = {
        "username": username,
        "email": email,
        "role": role
    }
    
    response = requests.post(url, headers=headers, data=json.dumps(payload))
    
    if response.status_code == 201:
        return response.json()
    else:
        raise Exception(f"API错误: {response.status_code} - {response.text}")

# 使用示例
try:
    user = create_user(
        api_key="your_api_key_here",
        username="johndoe",
        email="john.doe@example.com"
    )
    print(f"用户创建成功，ID: {user['id']}")
except Exception as e:
    print(f"错误: {e}")
```
