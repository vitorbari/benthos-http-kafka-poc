## About

This repo contains an example of how to use [Benthos](https://www.benthos.dev/) as an `http -> Kafka` server.

_Warning: this application is not production ready._

The application exposes an endpoint that publishes a message to Kafka containing the payload of the incoming JWT Bearer token.

## Usage

1. Spin up containers: `$ docker-compose up`

2. Start consuming messages: `$ kcat -C -b localhost:29092 -t users`. (Requires [kcat](https://github.com/edenhill/kcat)).

3. Send requests:

```
curl -v --request POST \
  --url http://127.0.0.1:4195/post \
  --header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c'

# No Authorization header should return bad request

curl -v --request POST \
  --url http://127.0.0.1:4195/post
```

## TODO

- Adjust Kafka [batching](https://www.benthos.dev/docs/components/outputs/kafka#batching) config
- Error handling for Kafka publishing
