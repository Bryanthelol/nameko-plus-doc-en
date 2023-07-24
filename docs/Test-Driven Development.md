---
hide:
  - footer
---

# Test-Driven Development

Writing unit tests is a highly rewarding task. Not only can it help you easily discover problems in your code, but it can also drive you to write more scalable and better code.

The Nameko microservices framework has excellent support for unit testing and integration testing:

- It provides utility methods to create Nameko service instances and containers.
- It adopts the concept of dependency injection, making dependencies easier to mock and replace.
- It integrates with the pytest library, allowing you to write tests directly using pytest syntax.

Without further ado, let's start writing unit tests.

## Unit Test First

After generating an 'example' directory as per the previous chapter "Quick Start", we can immediately use the `namekoplus` command to generate unit test case files in the 'example' directory.

```bash
namekoplus test-gen -e example -t unit
```

> The `-e` parameter specifies the directory of the microservice code file (must specify an existing Nameko service directory).
>
> The `-t` parameter specifies the type of unit test case file to be generated. Here we use `unit`, which stands for unit testing.

After running the above command in the project root directory, we can see that the file `test_service.py` has been generated:

```bash
project_root_dir
├── example
│   ├── …………
│   ├── __init__.py
│   ├── test_service.py
```

Opening the `test_service.py` file, we can see that there is already a test case inside:

```python

import pytest
from nameko.testing.services import worker_factory


@pytest.mark.parametrize(
    'value, expected',
    [
        ('John Doe', 'Hello, John Doe!'),
        ('', 'Hello, !'),
        ('Bryant', 'Hello, Bryant!'),
    ],
)
def test_example_service(value, expected):
    """
    Test example service.
    """
    # create worker with mock dependencies
    service = worker_factory(ServiceName)  # TODO replace ServiceName with the name of the service and import it

    # add side effects to the mock rpc dependency on the "remote" service
    service.remote.hello.side_effect = lambda name: "Hello, {}!".format(name)

    # test remote_hello business logic
    assert service.remote_hello(value) == expected
    service.remote.hello.assert_called_once_with(value)

```

We need to follow the instructions after #TODO, replace `ServiceName` with the service class name we are going to test, and import this service class at the top of the file.

Following the example from the previous chapter "Quick Start", `test_service.py` should be modified like this:

```python
…………

from example.rpc_demo import RpcCallerDemoService

…………

def test_example_service():

    …………
    
    service = worker_factory(RpcCallerDemoService)

    …………
```

After modifying the `test_service.py` file, we just need to run the `nameko test` command in the project root directory to see the test results:

```bash

========================================================================================================== test session starts ===========================================================================================================
platform darwin -- Python 3.11.4, pytest-7.4.0, pluggy-1.2.0
rootdir: /XXX/XXX/XXX/XXX
plugins: nameko-3.0.0rc11, anyio-3.7.1
collected 1 item

example/test_service.py .                                                                                                                                                                                                          [100%]

=========================================================================================================== 1 passed in 0.11s ============================================================================================================
```

So far, based on the `rpc_demo` service in the `example` directory, we have completed the generation and execution of a unit test case.

Moving forward, we can write test cases in the `test_service.py` file according to the actual project requirements, run the test once, get a failed result, then implement the corresponding service business logic, run the test again, until the test passes.

By integrating testing into our development process and maintaining a "test->development->test->development->test" cycle, the quality of our microservice code can be assured.