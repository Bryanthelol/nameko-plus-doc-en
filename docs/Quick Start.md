---
hide:
  - footer
---

# Quick Start

## Prerequisites

First, make sure you have Docker and Docker Compose installed in your environment.

Next, install the Namekoplus code library, which not only contains the dependencies of the Nameko microservice, but also provides a command-line tool for quick startup.

```bash
python3 -m pip install namekoplus
```

## Start a RabbitMQ

After installing namekoplus, we can start a RabbitMQ container that exposes ports 5672 and 15672 (15672 is the management interface port) with the following command:

```bash
namekoplus start -m rabbitmq 
```

After running the above command, we will soon see the output indicating that RabbitMQ has started successfully.

> The default username and password for the RabbitMQ management interface are "admin" and "admin".
> 
> If you wish to customize them, you can simply modify them in the RabbitMQ management interface later.
> 
> If you want to stop the RabbitMQ container later, you can use the command:
> 
> ```
> namekoplus stop -m rabbitmq
> ```

## Start Nameko microservices

Next, we will use the `namekoplus` command to initialize the template code for the Nameko microservice.

```
namekoplus init -d example -t demo
```

The `-d` parameter specifies the directory name where the Nameko code files are stored, and the `-t` parameter specifies the type of Nameko template code. In the above command, we used the `demo` type.

> In addition to the `demo` type, there are also `all|rpc|event|http|timer`, etc.
>
> The `rpc` type generates an example of the service-to-service RPC communication mode;
>
> The `event` type generates an example of publish-subscribe mode;
>
> The `http` type generates an example of an HTTP service;
>
> The `timer` type generates an example of a scheduled task;
>
> The `all` type generates an example that includes the `rpc|event|http|timer` types.

After running the command, we will see the newly created `example` directory in the current root directory. This directory contains the necessary code files to start the Nameko microservice.

Now let's start the Nameko microservice. From the root directory, use the command:

```
nameko run --config ./example/config.yml example.rpc_demo
```

If the service runs successfully, we will see output similar to the following:

```
starting services: rpc_caller_demo_service, rpc_responder_demo_service
```

## Call the Nameko microservice

In the previous step, we have already started two Nameko services, `rpc_caller_demo_service` and `rpc_responder_demo_service`.

Now we can use the Nameko microservice framework's shell tool to call this demo service.

Open a new command prompt window (while keeping the Nameko service window open, of course).

Use the following command to start the Nameko shell tool:

```
nameko shell --config ./example/config.yml
```

We will now enter the Nameko shell, where we can call the Nameko microservice's RPC interface:

```
n.rpc.rpc_responder_demo_service.hello("Bryant")
```

or

```
n.rpc.rpc_caller_demo_service.remote_hello("Bryant")
```

If both of these commands output `'Hello, Bryant!'`, then congratulations 🎉, you have successfully started and called a Nameko microservice!