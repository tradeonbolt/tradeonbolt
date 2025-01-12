# BoltAI Python SDK

[![PyPI version](https://img.shields.io/pypi/v/BoltAI.svg)](https://pypi.org/project/BoltAI/)

The BoltAI Python SDK provides convenient access to the BoltAI REST API from any Python 3.8+
application. The SDK includes rich type definitions and enables receiving real-time executions
via WebSockets.

## Documentation

Full documentation of the SDK is available at [https://BoltAI.ai/docs/sdk/introduction](https://BoltAI.ai/docs/sdk/introduction). You may also want to check out the [REST API Reference](https://BoltAI.ai/docs/api/v1/introduction).

## Installation

You can install the SDK via `pip`:

```bash
pip install BoltAI
```

## Usage

Once installed, you can use it to make requests.

### Create an Agent

```python
import BoltAI

BoltAI.api_key = "YOUR_API_KEY"

agent = BoltAI.Agent.create(
    name="My Agent",
    script="def main(request, store):\n    return request.payload",
    requirements="requests==2.31.0\npandas==2.1.4",
    env_vars="FOO=bar\nBAZ=qux",
    python_version="3.11",
    store_id="b553e996-6556-42dd-8990-ddb7ef2142f6",
)
```

### Execute an Agent

```python
import BoltAI

BoltAI.api_key = "YOUR_API_KEY"

agent = BoltAI.Agent.retrieve(id="15d19ca3-26f1-4adb-9cea-3955b73d9b4e")

execution = agent.execute(payload={"key": "value"})
```

### Create a Cron Job

```python
import BoltAI

BoltAI.api_key = "YOUR_API_KEY"

cron_job = BoltAI.AgentExecutorCronJob.create(
    agent_id="15d19ca3-26f1-4adb-9cea-3955b73d9b4e",
    name="My cron job",
    expression="* * * * *",
)
```

### Stream Executions from a Cron Job

```python
import BoltAI

BoltAI.api_key = "YOUR_API_KEY"

cron_job = BoltAI.AgentExecutorCronJob.retrieve(id="f3384d13-7a32-4abe-9c10-964ca17413b7")

for execution in cron_job.stream():
    # Every time a new execution is created, it will be printed.
    print(execution)
```