# sandcastle-sdk

**The AgentGateway Protocol — secure, scalable AI agent execution infrastructure.**

[![CI](https://github.com/Goldokpa/sandcastle-sdk/actions/workflows/ci.yml/badge.svg)](https://github.com/Goldokpa/sandcastle-sdk/actions)
[![PyPI](https://img.shields.io/pypi/v/sandcastle-sdk)](https://pypi.org/project/sandcastle-sdk/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## The problem

When an AI agent can execute code, call APIs, or access files, it runs in a process. That process typically contains everything that can cause serious damage: LLM API keys, database credentials, AWS tokens.

`sandcastle-sdk` solves this via the **AgentGateway Protocol**.

---

## Quick start

```bash
pip install sandcastle-sdk[openai]
```

```python
import asyncio
from openai import AsyncOpenAI
from sandcastle import DirectGateway, Message, Role

async def main():
    gateway = DirectGateway(
        llm_client=AsyncOpenAI(),
        model="gpt-4o",
    )
    response = await gateway.invoke_llm(
        new_messages=[Message(role=Role.USER, content="Hello!")]
    )
    print(response.message.content)
    print(f"Cost: ${response.cost_usd:.6f}")

asyncio.run(main())
```

## Moving to production

Change two lines. Your agent logic is untouched.

```python
# Before (local)
from sandcastle import DirectGateway
gateway = DirectGateway(llm_client=AsyncOpenAI(), model="gpt-4o")

# After (production — zero secrets in agent)
from sandcastle import ControlPlaneGateway
gateway = ControlPlaneGateway()
```

---

## Installation

```bash
pip install sandcastle-sdk             # core
pip install sandcastle-sdk[openai]     # with OpenAI
pip install sandcastle-sdk[anthropic]   # with Anthropic
pip install sandcastle-sdk[all]         # both
```

**Requirements:** Python 3.10+

---

## License

MIT © Gold Okpa
