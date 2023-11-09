# Simple todo API

Built using instructions in [blog](https://www.sarvika.com/2019/11/21/build-scalable-web-application-in-go/) "Building a scalable web application in Go"

## Downloading and running

Assuming that you have `$GOPATH` set-up

```shell
$ go get -u github.com/tanmay-pnaik/golang-todo-app-lumos
$ cd $GOPATH/src/github.com/tanmay-pnaik/golang-todo-app-lumos
$ dep ensure
$ docker-compose up
```

## APIs

### `GET /api/todos/` : List all todo items

```shell
$ curl --silent localhost:8080/api/todos/ | jq .
```

```json
[
  {
    "completed": true,
    "title": "Todo #1",
    "id": 1
  }
]
```

### `GET /api/todos/:id`: List single todo item

```shell
$ curl --silent localhost:8080/api/todos/1 | jq .
```

```json
{
  "completed": false,
  "title": "Todo #1",
  "id": 1
}
```

### `POST /api/todos/` : Create todo item

```shell
$ curl --silent -X POST localhost:8080/api/todos/ -d '{"title": "Todo #1"}'  | jq .
```

```json
{
  "completed": false,
  "title": "Todo #1",
  "id": 1
}
```

### `PATCH /api/todos/:id` : Update a single todo item

```shell
$ curl --silent -X PATCH localhost:8080/api/todos/1 -d '{"completed": true}'  | jq .
```

```json
{
  "completed": true,
  "title": "Todo #1",
  "id": 1
}
```

```shell
$ curl --silent -X PATCH localhost:8080/api/todos/2 -d '{"title": "Changed title #2"}'  | jq .
```

```json

{
  "completed": false,
  "title": "Changed title #2",
  "id": 2
}
```

### `DELETE /api/todos/:id` : Delete single todo item

```shell
$ curl --silent -X DELETE localhost:8080/api/todos/1  | jq .
```
```shell
$ curl --silent localhost:8080/api/todos/ | jq .
```

```json
[
  {
    "completed": false,
    "title": "Changed title #2",
    "id": 2
  }
]
```