## [Figma MCP Agent](https://github.com/Coral-Protocol/Coral-FigmaMCP-Agent)

The Figma MCP Agent is an open-source agent designed to  bring Figma MCP features directly into your agentic system by providing important design information and context to AI agents generating code from Figma design files.

## Responsibility
The Figma MCP Agent is capable of extracting code, variable definitions, and connection mappings from Figma design nodes, generating images from design elements, and creating design system rules tailored to client programming languages and frameworks.

Below are the tools and their descriptions:

1. get_code: This tool turns a Figma design into code, usually in React with Tailwind styling. It tracks the app and coding styles you’re using (like JavaScript or React) for records. Usage: Ask for different styles, like “Make my Figma design in Vue” or “Use plain HTML and CSS.” You can also use your own components by saying, “Use my components from src/components/ui.” Just select your design in Figma or share a link first. Check Figma’s guide to set up Code Connect for reusing components.  

2. get_variable_defs: This tool lists design details like colors or spacing used in your Figma design. It keeps track of the app and coding styles for logging. Usage: Ask “What details are in my Figma design?” for all details, “What colors are used?” for specific ones, or “Show names and values of design details” to see everything clearly.  

3. get_code_connect_map: This tool links your Figma design to the code components in your project, showing where each component lives (like a file path) and its name. It tracks app and coding styles for records. Usage: Use it to find which code matches your Figma design, making sure the right components are used when building.  

4. get_image: This tool takes a screenshot of your Figma design to keep its look accurate. It tracks the app and coding styles for logging. You need to turn it on in Figma’s settings (Preferences > Dev Mode > Enable get_image). Usage: Enable it to capture your design’s look; keep it on unless you’re saving on limits.  

NOTE: Ensure to run Figma Dev Mode MCP Server before using this agent by following: [Figma MCP Documentation](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)

## Details
- **Framework**: LangChain
- **Tools used**: Figma MCP Tools(4 tools), Coral Server Tools
- **AI model**: OpenAI GPT-4o
- **Date added**: June 4, 2025
- **Reference**: [Figma MCP Documentation](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)
- **License**: MIT

## Setup the Agent

### 1. Clone & Install Dependencies

<details>

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system. If you are trying to run Open Deep Research agent and require an input, you can either create your agent which communicates on the coral server or run and register the [Interface Agent](https://github.com/Coral-Protocol/Coral-Interface-Agent) on the Coral Server  


```bash
# In a new terminal clone the repository:
git clone https://github.com/Coral-Protocol/Coral-FigmaMCP-Agent.git

# Navigate to the project directory:
cd Coral-FigmaMCP-Agent

# Download and run the UV installer, setting the installation directory to the current one
curl -LsSf https://astral.sh/uv/install.sh | env UV_INSTALL_DIR=$(pwd) sh

# Create a virtual environment named `.venv` using UV
uv venv .venv

# Activate the virtual environment
source .venv/bin/activate

# install uv
pip install uv

# Install dependencies from `pyproject.toml` using `uv`:
uv sync
```

</details>

### 2. Configure Environment Variables

<details>

Get the API Key:
[OpenAI](https://platform.openai.com/api-keys) || 

```bash
# Create .env file in project root
cp -r .env_sample .env
```

Check if the .env file has correct URL for Coral Server and adjust the parameters accordingly.

</details>

## Run the Agent

You can run in either of the below modes to get your system running.  

- The Executable Model is part of the Coral Protocol Orchestrator which works with [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio).  
- The Dev Mode allows the Coral Server and all agents to be seperately running on each terminal without UI support.  

### 1. Executable Mode

Checkout: [How to Build a Multi-Agent System with Awesome Open Source Agents using Coral Protocol](https://github.com/Coral-Protocol/existing-agent-sessions-tutorial-private-temp) and update the file: `coral-server/src/main/resources/application.yaml` with the details below, then run the [Coral Server](https://github.com/Coral-Protocol/coral-server) and [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio). You do not need to set up the `.env` in the project directory for running in this mode; it will be captured through the variables below.

<details>

For Linux or MAC:

```bash
registry:
  # ... your other agents
  figmamcp_agent:
    options:
      - name: "MODEL_API_KEY"
        type: "string"
        description: "API key for the service"
      - name: "MODEL_NAME"
        type: "string"
        description: "What model to use (e.g 'gpt-4.1-mini')"
        default: "gpt-4.1-mini"
      - name: "MODEL_PROVIDER"
        type: "string"
        description: "What model provider to use (e.g 'openai', etc)"
        default: "openai"
      - name: "MODEL_MAX_TOKENS"
        type: "string"
        description: "Max tokens to use"
        default: "16000"
      - name: "MODEL_TEMPERATURE"
        type: "string"
        description: "What model temperature to use"
        default: "0.0"
    runtime:
      type: "executable"
      command: ["bash", "-c", "<replace with path to this agent>/run_agent.sh main.py"]
      environment:
        - option: "MODEL_API_KEY"
        - option: "MODEL_NAME"
        - option: "MODEL_PROVIDER"
        - option: "MODEL_MAX_TOKENS"
        - option: "MODEL_TEMPERATURE"

```
For Windows, create a powershell command (run_agent.ps1) and run:

```bash
command: ["powershell","-ExecutionPolicy", "Bypass", "-File", "${PROJECT_DIR}/run_agent.ps1","main.py"]
```

</details>

### 2. Dev Mode

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system and run below command in a separate terminal.

<details>

```bash
# Run the agent using `uv`:
uv run python main.py
```

You can view the agents running in Dev Mode using the [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio) by running it separately in a new terminal.

</details>


## Example

<details>

```bash
# Input:

#Output:

```

</details>

### Creator Details
- **Name**: Suman Deb
- **Affiliation**: Coral Protocol
- **Contact**: [Discord](https://discord.com/invite/Xjm892dtt3)

