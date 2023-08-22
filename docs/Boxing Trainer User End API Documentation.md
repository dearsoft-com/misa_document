## 3.1 Authentication





### 3.1.1 Log In

```
POST /api/login
```



#### Request: String in HTTP Header, Parameter(s) in HTTP Body

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |
| `Accept` | `text` | `application/json` |

```
Accept: application/json
```

Body (raw)


```json
{
  "login_name": "0929854547",
  "password": "abcd1234"
}
```

#### Response: 200 OK

```
Status: 200 OK
```
```json
{
  "user_id": "0s0rbdjf9u8wu0nv",
  "login_name": "0929854547",
  "mobile": "0929854547",
  "email": "fido@foo.bar",
  "nick_name": "John",
  "gender": "male",
  "birth_year": 1990,
  "access_token": "xxx"
}
```
#### Response: 401 Unauthorized

```
Status: 401 Unauthorized
```



### 3.1.2 Log Out

```
POST /api/logout
```



#### Request: String in HTTP Header

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


#### Response: 204 No Content

```
Status: 204 No Content
```



### 3.1.3 Check Login

```
GET /api/login
```



#### Request: String in HTTP Header

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


#### Response: 200 OK

```
Status: 200 OK
```
```json
{
  "user_id": "0s0rbdjf9u8wu0nv",
  "login_name": "0929854547",
  "mobile": "0929854547",
  "email": "fido@foo.bar",
  "nick_name": "John",
  "gender": "male",
  "birth_year": 1990
}
```
#### Response: 401 Unauthorized

```
Status: 401 Unauthorized
```



### 3.1.4 Register

```
POST /api/register
```



#### Request: String in HTTP Header, Parameter(s) in HTTP Body

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


Body (raw)


```json
{
  "login_name": "0929854547",
  "mobile": "0929854547",
  "email": "fido@foo.bar",
  "nick_name": "John",
  "gender": "male", //male|female
  "birth_year": 1990
}
```

#### Response: 204 No Content

```
Status: 204 No Content
```
```

```


### 3.1.5 Apply Forgot Password

```
POST /api/forgot-password
```



#### Request: String in HTTP Header, Parameter(s) in HTTP Body

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


Body (raw)


```json
{
  "email": "fido@foo.bar"
}
```

#### Response: 204 No Content

```
Status: 204 No Content
```



### 3.1.6 Reset Password

```
POST /api/reset-password
```



#### Request: String in HTTP Header, Parameter(s) in HTTP Body

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


Body (raw)


```json
{
  "str1": "", // given by the link in reset-password email
  "str2": "", // given by the link in reset-password email
  "password": "1234abcd"
}
```

#### Response: 204 No Content

```
Status: 204 No Content
```



### 3.1.7 Edit User Info

```
PUT /api/user
```



#### Request: String in HTTP Header, Parameter(s) in HTTP Body

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


Body (raw)


```json
{
  "nick_name": "John",
  "gender": "male",
  "birth_year": 1990
}
```

#### Response: 204 No Content

```
Status: 204 No Content
```




## 3.2 Personal Record





### 3.2.1 Record Statistic

```
GET /api/record-statistic
```



#### Request: String in HTTP Header, Parameter(s) in Query String

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


Query String

| Name | Type | Description |
| ---- | ---- | ----------- |
| `startAt` | `text` | undefined |
| `endAt` | `text` | undefined |
| `mode` | `text` | 1=free_fight&2=punch_challenge&3=video_training |
| `field` | `text` | undefined |

```

startAt: 1690848000000
endAt: 1693440000000
mode: 1
field: average_power
```

#### Response: 200 OK

```
Status: 200 OK
```
```json
[
  {
    "time": 1691716394913,
    "value": 12
  },
  {
    "time": 1691697914896,
    "value": 18
  },
  {
    "time": 1691670639226,
    "value": 12
  },
  {
    "time": 1690945292141,
    "value": 14
  },
  {
    "time": 1692732925409,
    "value": 11
  },
  {
    "time": 1692977507743,
    "value": 12
  },
  {
    "time": 1691718149610,
    "value": 17
  },
  {
    "time": 1693225968004,
    "value": 11
  },
  {
    "time": 1692662705127,
    "value": 16
  },
  {
    "time": 1691137865534,
    "value": 12
  }
]
```


### 3.2.2 Free Fight Record

```
GET /api/free-record
```



#### Request: String in HTTP Header, Parameter(s) in Query String

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |
| `Accept` | `text` | `application/json` |
| `Content-Type` | `text` | `application/json` |

```
Accept: application/json
Content-Type: application/json
```

Query String

| Name | Type | Description |
| ---- | ---- | ----------- |
| `offset` | `text` | undefined |
| `limit` | `text` | undefined |
| `startAt` | `text` | undefined |
| `endAt` | `text` | undefined |

```

offset: 0
limit: 10
startAt: 1690848000000
endAt: 1693440000000
```

#### Response: 200 OK

```
Status: 200 OK
```
```json
{
  "total": 3,
  "data": [
    {
      "id": 1691824450000,
      "date": "2023-08-12 07:14:10",
      "left_hook": 20,
      "left_punch": 20,
      "left_uppercut": 20,
      "right_hook": 20,
      "right_punch": 20,
      "right_uppercut": 20,
      "average_cadance": 20,
      "maximum_cadance": 20,
      "average_power": 20,
      "maximum_power": 20
    },
    {
      "id": 1691651650000,
      "date": "2023-08-10 07:14:10",
      "left_hook": 20,
      "left_punch": 20,
      "left_uppercut": 20,
      "right_hook": 20,
      "right_punch": 20,
      "right_uppercut": 20,
      "average_cadance": 20,
      "maximum_cadance": 20,
      "average_power": 20,
      "maximum_power": 20
    },
    {
      "id": 1691046850000,
      "date": "2023-08-03 07:14:10",
      "left_hook": 20,
      "left_punch": 20,
      "left_uppercut": 20,
      "right_hook": 20,
      "right_punch": 20,
      "right_uppercut": 20,
      "average_cadance": 20,
      "maximum_cadance": 20,
      "average_power": 20,
      "maximum_power": 20
    }
  ]
}
```


### 3.2.4 Video Training Record

```
GET /api/video-record
```



#### Request: String in HTTP Header, Parameter(s) in Query String

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |
| `Accept` | `text` | `application/json` |
| `Content-Type` | `text` | `application/json` |

```
Accept: application/json
Content-Type: application/json
```

Query String

| Name | Type | Description |
| ---- | ---- | ----------- |
| `offset` | `text` | undefined |
| `limit` | `text` | undefined |
| `startAt` | `text` | optional |
| `endAt` | `text` | optional |

```

offset: 0
limit: 10
startAt: 1690848000000
endAt: 1693440000000
```

#### Response: 200 OK

```
Status: 200 OK
```
```json
{
  "total": 3,
  "data": [
    {
      "id": 1691824450000,
      "date": "2023-08-12 07:14:10",
      "strike_number": 20,
      "missed_number": 5,
      "strike_rate": 80,
      "total_score": 80,
      "average_power": 12,
      "average_cadance": 12
    },
    {
      "id": 1691651650000,
      "date": "2023-08-10 07:14:10",
      "strike_number": 20,
      "missed_number": 5,
      "strike_rate": 80,
      "total_score": 80,
      "average_power": 12,
      "average_cadance": 12
    },
    {
      "id": 1691046850000,
      "date": "2023-08-03 07:14:10",
      "strike_number": 20,
      "missed_number": 5,
      "strike_rate": 80,
      "total_score": 80,
      "average_power": 12,
      "average_cadance": 12
    }
  ]
}
```


### 3.2.3 Punch Challenge Record

```
GET /api/challenge-record
```



#### Request: String in HTTP Header, Parameter(s) in Query String

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |
| `Accept` | `text` | `application/json` |
| `Content-Type` | `text` | `application/json` |

```
Accept: application/json
Content-Type: application/json
```

Query String

| Name | Type | Description |
| ---- | ---- | ----------- |
| `offset` | `text` | undefined |
| `limit` | `text` | undefined |
| `startAt` | `text` | undefined |
| `endAt` | `text` | undefined |

```

offset: 0
limit: 10
startAt: 1690848000000
endAt: 1693440000000
```

#### Response: 200 OK

```
Status: 200 OK
```
```json
{
  "total": 3,
  "data": [
    {
      "id": 1691824450000,
      "date": "2023-08-12 07:14:10",
      "good_punch": 20,
      "great_punch": 20,
      "miss_punch": 20,
      "agility": 20,
      "reaction": 20,
      "concentration": 20,
      "average_cadance": 20,
      "average_power": 20,
      "maximum_cadance": 20,
      "maximum_power": 20
    },
    {
      "id": 1691651650000,
      "date": "2023-08-10 07:14:10",
      "good_punch": 20,
      "great_punch": 20,
      "miss_punch": 20,
      "agility": 20,
      "reaction": 20,
      "concentration": 20,
      "average_cadance": 20,
      "average_power": 20,
      "maximum_cadance": 20,
      "maximum_power": 20
    },
    {
      "id": 1691046850000,
      "date": "2023-08-03 07:14:10",
      "good_punch": 20,
      "great_punch": 20,
      "miss_punch": 20,
      "agility": 20,
      "reaction": 20,
      "concentration": 20,
      "average_cadance": 20,
      "average_power": 20,
      "maximum_cadance": 20,
      "maximum_power": 20
    }
  ]
}
```



## 3.3 Leaderboard





### 3.3.1 Leaderboard

```
GET /api/leaderboard
```



#### Request: String in HTTP Header, Parameter(s) in Query String

Headers

| Name | Type | Description |
| ---- | ---- | ----------- |
| `Authorization` | `string` | **(必填)** bearer token |


Query String

| Name | Type | Description |
| ---- | ---- | ----------- |
| `mode` | `text` | 1=free_fight&2=punch_challenge&3=video_training |
| `field` | `text` | undefined |

```

mode: 1
field: average_power
```

#### Response: 200 OK

```
Status: 200 OK
```
```json
[
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  },
  {
    "rank": 1,
    "name": "Tommy456",
    "value": "23"
  }
]
```



