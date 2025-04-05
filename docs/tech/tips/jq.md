# JSON processing in shell with `jq`

`jq` is a command line JSON processor which will help you pretty-print and filter a JSON in a terminal

### Format JSON

```sh
echo '{"user": {"name": "Elie", "age": 29}}' | jq .
```

### Extract specific fields

```sh
echo '{"user": {"name": "Elie", "age": 29}}' | jq '.user.name'
```

### Extract fields from an array

```sh
echo '[{"project": "frontend", "status": "ok"}, {"project": "backend", "status": "ko"}]' | jq '.[] | .project'
```

### Filter an array

```sh
echo '[{"project": "frontend", "status": "ok"}, {"project": "backend", "status": "ko"}]' | jq '.[] | select(.status=="ok")'
```

### Transform JSON

```sh
echo '{"firstName": "Elie", "lastName": "Daher"}' | jq '{fullName: (.firstName + " " + .lastName)}'
```

`jq` helps specially when we call an endpoint or a cli that returns a JSON response. 
