# Ollama Tutorial

A comprehensive tutorial repository demonstrating how to use Ollama, an open-source LLM framework, with Python. This repository contains multiple notebooks showcasing different features and use cases.

## Overview

Ollama is a tool for running large language models locally. This project demonstrates various ways to interact with Ollama models, including direct API calls, LangChain integration, REST API usage, and tool calling capabilities.

## Notebooks

### 1. **ollama.ipynb**
Basic introduction to Ollama with the `llama3.2` model.
- Loading and running the Ollama model
- Basic chat interactions
- Understanding the response structure

### 2. **ollama_Cloude.ipynb**
Advanced Ollama usage with features like:
- Extended conversations with multiple turns
- Response formatting
- Model-specific configurations

### 3. **tool_calling.ipynb**
Demonstrates how to use Ollama with function/tool calling:
- Define custom tools (functions) for the model to call
- Inventory management system example
- Loyalty discount calculation
- Tool calling loop: call model → execute tool → return result
- Features:
  - `check_inventory(product_name)`: Get stock and price for a product
  - `calculate_loyalty_discount(base_price, years_as_customer)`: Calculate discounted price based on loyalty

### 4. **ollama_langchain.ipynb**
Integration with LangChain framework:
- Using LangChain with Ollama backend
- Chat models and prompts
- Chain-based workflows
- Simplified model interactions through LangChain abstractions

### 5. **ollama_RESTapi.ipynb**
Interacting with Ollama through its REST API:
- Making HTTP requests to Ollama endpoints
- Understanding the API response structure
- Comparing REST API with direct library usage

## Requirements

### System
- Ollama installed and running (download from [ollama.ai](https://ollama.ai))
- Python 3.8+

### Python Dependencies
```bash
pip install ollama langchain httpx jupyter ipython
```

### Virtual Environment
The project includes a virtual environment (`ola_venv/`) with all dependencies pre-installed.

## Setup & Installation

1. **Clone the repository**
```bash
git clone https://github.com/vad-007/Ollama_tutorial.git
cd Ollama_tutorial
```

2. **Activate virtual environment**
```bash
# Windows
ola_venv\Scripts\activate

# macOS/Linux
source ola_venv/bin/activate
```

3. **Start Ollama**
```bash
ollama serve
```

4. **Run Jupyter Notebook**
```bash
jupyter notebook
```

## Usage Examples

### Basic Chat
```python
import ollama

response = ollama.chat(
    model="llama3.2:latest",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response["message"]["content"])
```

### Tool Calling
```python
# Define tools and let the model call them
tools = [
    {
        "type": "function",
        "function": {
            "name": "check_inventory",
            "description": "Check product stock",
            "parameters": {
                "type": "object",
                "properties": {"product_name": {"type": "string"}},
                "required": ["product_name"]
            }
        }
    }
]

response = ollama.chat(
    model="llama3.2:latest",
    messages=[{"role": "user", "content": "How many laptops in stock?"}],
    tools=tools
)
```

### LangChain Integration
```python
from langchain_ollama import OllamaLLM

model = OllamaLLM(model="llama3.2:latest")
response = model.invoke("What is machine learning?")
```

## Key Concepts

### Function/Tool Calling
The tool calling notebook demonstrates how to:
1. Define custom functions
2. Create tool definitions in the Ollama schema format
3. Map tool names to Python functions
4. Handle model tool requests
5. Execute tools and return results to the model

### Type Conversion
Important: When the model calls tools with string arguments, explicit type conversion is needed:
```python
if 'base_price' in tool_args:
    tool_args['base_price'] = float(tool_args['base_price'])
```

## Models Used

- **llama3.2:latest** - The primary model used throughout the tutorials

To use different models, pull them with:
```bash
ollama pull model_name
```

## Troubleshooting

### Model Not Found
```bash
ollama pull llama3.2:latest
```

### Connection Issues
- Ensure Ollama is running: `ollama serve`
- Check if running on default port (11434)

### Type Errors in Tool Calling
- Ensure arguments are converted to correct types before function calls
- Validate tool schemas match function signatures

## Resources

- [Ollama Official Site](https://ollama.ai)
- [Ollama GitHub Repository](https://github.com/ollama/ollama)
- [LangChain Documentation](https://langchain.readthedocs.io/)
- [LangChain Ollama Integration](https://python.langchain.com/docs/integrations/llms/ollama)

## License

This project is provided as-is for educational purposes.

## Connect

- **LinkedIn**: [Professional Profile](linkedin.jpg)
- **AI Learning**: See `Green_AI.jpg` for more information

---

**Last Updated**: April 13, 2026
