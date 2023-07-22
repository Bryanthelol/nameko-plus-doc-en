---
hide:
  - footer
---

# Quick Start

## Preparation

1. Make sure that the current environment has docker and docker compose.
2. Install the namekoplus code library.

## Start a RabbitMQ

1. Install namekoplus.
2. Run the following command to start a RabbitMQ container:

```bash
namekoplus start -m rabbitmq
```

## Start Nameko Microservice

1. Use the `namekoplus` command to initialize the template code for the Nameko microservice.

```
namekoplus init -d example -t demo
```

2. Start the Nameko microservice.

```
nameko run --config ./example/config.yml example.rpc_demo
```

## Call Nameko Microservice

1. Use the nameko shell tool to call the demo service.

```
nameko shell --config ./example/config.yml
```

2. Call the RPC interface provided by the nameko microservice.

```
n.rpc.rpc_responder_demo_service.hello("Bryant")
```

or

```
n.rpc.rpc_caller_demo_service.remote_hello("Bryant")
```

If both of these commands output `'Hello, Bryant!'`, then congratulations 🎉, you have successfully started and called a Nameko microservice!