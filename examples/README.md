# Example Agents - Framework Support Demonstration

This directory contains example agents demonstrating Agentscan's support for various AI agent frameworks.

## Framework Examples

### ✓ LangChain
File: `langchain_agent.py`

Demonstrates a LangChain agent with:
- LangChain imports (`from langchain.agents import ...`)
- Governance patterns (logging, error handling, env vars, checkpointing)
- Framework detection: Detected as `langchain`

Test:
```bash
python analyze.py examples/langchain_agent.py
```

### ✓ LangGraph
File: `langgraph_agent.py`

Demonstrates a LangGraph agent with:
- LangGraph imports (`from langgraph.graph import StateGraph`)
- StateGraph usage for agent orchestration
- Governance patterns (logging, error handling, env vars, checkpointing)
- Framework detection: Detected as `langgraph` or `langchain` (depending on imports)

Test:
```bash
python analyze.py examples/langgraph_agent.py
```

### ✓ CrewAI
File: `crewai_agent.py`

Demonstrates a CrewAI agent with:
- CrewAI imports (`from crewai import Agent, Task, Crew`)
- Multi-agent orchestration
- Governance patterns (logging, error handling, env vars, checkpointing)
- Framework detection: Detected as `crewai`

Test:
```bash
python analyze.py examples/crewai_agent.py
```

### ✓ OpenAI Assistants API
File: `openai_assistants_agent.py`

Demonstrates an OpenAI Assistants API agent with:
- OpenAI beta imports (`from openai import beta`)
- Assistant and thread management
- Governance patterns (logging, error handling, env vars, checkpointing)
- Framework detection: Detected as `openai_assistants`

Test:
```bash
python analyze.py examples/openai_assistants_agent.py
```

### ✓ Anthropic Claude API
File: `anthropic_claude_agent.py`

Demonstrates an Anthropic Claude API agent with:
- Anthropic imports (`from anthropic import Anthropic`)
- Claude API usage
- Governance patterns (logging, error handling, env vars, checkpointing)
- Framework detection: Detected as `anthropic`

Test:
```bash
python analyze.py examples/anthropic_claude_agent.py
```

### ✓ Custom Python Agent
File: `custom_python_agent.py`

Demonstrates a custom Python agent with:
- No specific framework (uses requests library directly)
- Custom LLM integration patterns
- Governance patterns (logging, error handling, env vars, checkpointing)
- Framework detection: Detected as `custom` (based on agent/LLM patterns)

Test:
```bash
python analyze.py examples/custom_python_agent.py
```

## How Agentscan Works with Your Frameworks

Agentscan is framework-agnostic. It works by:

1. AST Parsing: Parses Python source code into Abstract Syntax Trees
2. Pattern Detection: Detects governance patterns (logging, secrets, error handling, etc.) regardless of framework
3. Framework Detection: Informational only - identifies which framework is used, but doesn't require it

What Gets Detected:
- ✓ Logging imports and calls (`import logging`, `logger.info()`)
- ✓ Hardcoded secrets (`api_key = "sk-..."`)
- ✓ Environment variable usage (`os.getenv()`)
- ✓ Error handling (`try/except` blocks)
- ✓ Checkpointing (serialization calls like `json.dump()`, `pickle.dump()`)
- ✓ PII handling (if using presidio/spacy)
- ✓ Monitoring (if using prometheus/grafana/etc.)

What Doesn't Matter:
- Which framework you use (LangChain, CrewAI, custom, etc.)
- Framework-specific APIs or patterns
- How you structure your agent code

## Testing All Examples

Run all examples to verify framework support:

```bash
# Test all framework examples
for file in examples/*_agent.py; do
    echo "=== Analyzing $file ==="
    python analyze.py "$file" 2>&1 | grep -E "(Agent Framework|Patterns Detected)"
    echo ""
done
```

## Notes

- These examples may not run without proper API keys
- Framework detection is informational - governance pattern detection works regardless
- Agentscan analyzes code structure, not runtime behavior
- Custom implementations may not be detected
