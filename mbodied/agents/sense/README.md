# Sensory Agent

The `SensoryAgent` is an abstract base class designed for creating agents that interact with various sensory components, such as images and/or depth maps. These agents can connect to different backends to process sensory data, enabling tasks like object detection, depth estimation, and more.

## Key Features

- **Backend Flexibility**: Natively supports multiple API services including OpenAI, Anthropic, vLLM, Ollama, HTTPX, and any Gradio endpoints. More integrations are coming soon!
- **Extensibility**: The `SensoryAgent` class provides a flexible template for building custom sensory agents tailored to specific tasks or services.

## Quick Start

### 1. Import the Sensory Agent

Begin by importing the `SensoryAgent` class from the `mbodied` package.

```python
from mbodied.agents.sense.sensory_agent import SensoryAgent
```

### 2. Define a Custom Sensory Agent

Create a subclass of `SensoryAgent` to define a custom sensory agent. For example,


```python
class MySensoryAgent(SensoryAgent):
    
    def __init__(
        self,
        model_src="https://api.mbodi.ai/sense/",
        model_kwargs=None,
        **kwargs,
    ):
        super().__init__(
            model_src=model_src,
            model_kwargs=model_kwargs,
            **kwargs,
        )

    def act(self, *args, **kwargs) -> Any:
        if self.actor is None:
            raise ValueError("Remote actor for agent not initialized.")
        response = self.actor.predict(*args, **kwargs)
        return response
```

In this example, the `MySensoryAgent` class is configured to interact with a Gradio endpoint at the specified `model_src`. The `act` method sends data to the backend and returns the response.


### 3. Use the Custom Agent in Your Script

In another script, you can import and use your custom sensory agent as follows:

```python
from path.to.your.agent import MySensoryAgent

# Initialize the agent
agent = MySensoryAgent()

# Use the agent to process data
response = agent.act(image=your_image_data)
```

Replace `your_image_data` with the actual image or sensory data you wish to process. The `act` method sends the data to the backend and returns the result.

