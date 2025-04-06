# API Conventions

## HTTP request methods 

| Method   | Description                            |
| -------- | -------------------------------------- |
| `GET`    | Retrieve data (should not modify data) |
| `POST`   | Create a new resource                  |
| `PUT`    | Modify/Update an existing resource     |
| `PATCH`  | Modify part of an existing resource    |
| `DELETE` | Delete an existing resources           |

## Best practices 

### Plural nouns 
It helps ensure consistency and better reflects the possibility of the endpoint returning multiple resources

⛔ `GET /category`
✅ `GET /categories`

⛔ `GET /user`
✅ `GET /users`

### Separate words with hyphens 
Use hyphens `-` to improve the readability of URIs, do not use underscores `_`

⛔ `GET /managed_devices`
✅ `GET /myfolders`

⛔ `GET /managed-devices`
✅ `GET /my-folders`

### Use lowercase letters
Lowercase letters should be consistently preferred in URI paths

⛔ `GET /Categories`
✅ `GET /categories`

⛔ `GET /USERS`
✅ `GET /users`

### Use path variables for singleton resource 

```
GET /categories
```
_will return a collection of resource categories_

```
GET /categories/{id}
```
_will return a singleton resource a category_

### Use query param to filter a collection

⛔ `GET /categories/search-by-name/{name}`
✅ `GET /categories?name={name}`

⛔ `GET /users/username/{username}`
✅ `GET /users?username={username}`

### Sub resources

```
GET /categories/{id}/posts
```
_will return the list of posts per a category_

```
GET /posts/{id}/categories
```
_will return the list of categories per a post_

### Version your endpoints
Helps to easily manage changes and updates to an API while still maintaining backward compatibility

```
GET /v1/categories
```

```
GET /v2/categories
```

### Do not use verbs in the URI 
HTTP methods (GET, POST, PUT, DELETE, etc.) are used to perform actions on those resources, effectively acting as verbs

⛔ `POST /v1/categories/create`
✅ `POST /v1/categories`

⛔ `POST /v1/categories/update`
✅ `PUT /v1/categories`

#### Use Cases

| Endpoint                        | Use Case                                      |
| ------------------------------- | --------------------------------------------- |
| `GET /v1/categories`            | Get all categories                            |
| `GET /v1/categories/{id}`       | Get category by id                            |
| `GET /v1/categories/{id}/posts` | Get all post of a certain categories          |
| `GET /v1/posts?date=20-01-2024` | Search posts by created date                  |
| `POST /v1/categories`           | Create a new category                         |
| `PUT /v1/categories/{id}`       | Update an existing category                   |
| `PATCH /v1/categories/{id}`     | Update a sub property of an existing category |
| `DELETE /v1/categories/{id}`    | Delete an existing category by id             |

## HTTP Status Code

HTTP defines these standard status codes that can be used to convey the results of a client’s requests. They are divided into five categories

| Status | Description   |
| ------ | ------------- |
| `1xx`  | Informational |
| `2xx`  | Success       |
| `3xx`  | Redirection   |
| `4xx`  | Client error  |
| `5xx`  | Server error  |

Here are the most common HTTP status codes 

| Status                       | Description                                            |
| ---------------------------- | ------------------------------------------------------ |
| `200` Ok                     | Request was successful                                 |
| `201` Created                | Request was successful and a new resource was created  |
| `400` Bad request            | Server couldn’t process the request to a client error  |
| `500` Internal server error  | Server encountered an unexpected exception             |
| `403` Forbidden              | User don’t have the permissions to access the resource |
| `404` Not found              | Resource not found                                     |
| `503` Service unavailable    | Server not able to handle requests                     |
