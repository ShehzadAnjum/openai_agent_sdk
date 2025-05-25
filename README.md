# openai_agent_sdk
Learning path of Open AI Agent SDK

## Installation

```bash
uv init <project name>
uv venv && .venv\Scripts\activate
```

```bash
# adding Openai Agent SDK with uv
uv add openai-agents
```

```bash
# OR simply with pip, if not using UV  
pip install openai-agents
```

## Basic Working Code
```bash
import os
from dotenv import load_dotenv, find_dotenv
from agents import (
    Agent, 
    Runner, 
    AsyncOpenAI,
    OpenAIChatCompletionsModel,
    set_tracing_disabled,
    set_default_openai_client
)

_ = load_dotenv(find_dotenv())

gemini_api_key = os.getenv("GEMINI_API_KEY")
# don't forget to put your GEMINI_API_KEY in the .env file located at the root of ur project
# print("Gemini API Key: ", gemini_api_key)

set_tracing_disabled(True)
#Reference: https://ai.google.dev/gemini-api/docs/openai
external_client = AsyncOpenAI(
    api_key=gemini_api_key,
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/",
)

model = OpenAIChatCompletionsModel(
    model="gemini-2.0-flash",
    openai_client=external_client
)

agent = Agent(
    name="Assistan", 
    instructions = "You are a helpful assistant",
    model=model
    )

result = Runner.run_sync(agent, "Write a haiku about recursion in programming." )

print(result.final_output)
```
