# Making HTTP requests with curl

`curl` is a command-line tool used to transfer data to or from a server using HTTP. It’s especially handy for APIs.


```sh
curl https://example.com
```

This command will send an HTTP GET request to https://example.com and display the HTML content of the response in your terminal.

## `-X` or `--request`: Specifies the HTTP method to use (e.g., GET, POST, PUT, DELETE)

```sh
curl -X POST https://api.example.com/users
```

## `-d` or `--data`: Sends data in the request body

```sh
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"Hello","body":"Mini blog rocks","userId":1}'
```

## `-H` or `--header`: Adds custom headers to the request

```sh
curl -H "Authorization: Bearer <your_token>" https://api.example.com/profile
```

## `-o` or `--output`: Saves the downloaded content to a file

```sh
curl https://example.com/image.png -o image.png
```

Mastering `curl` gives you an edge when working with APIs, scripts, and backend debugging.