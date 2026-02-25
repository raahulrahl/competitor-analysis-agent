<p align="center">
  <img src="https://raw.githubusercontent.com/getbindu/create-bindu-agent/refs/heads/main/assets/light.svg" alt="bindu Logo" width="200">
</p>

<h1 align="center">🔬 AI-Powered Competitive Intelligence Agent</h1>
<h3 align="center">Expert Competitor Analysis and Strategic Insights</h3>

<p align="center">
  <strong>AI-driven competitor research and analysis for informed business decisions</strong><br/>
  A production-ready agent that performs deep competitive intelligence using web search and scraping
</p>

<p align="center">
  <a href="https://github.com/Paraschamoli/competitor-analysis-agent">
    <img src="https://img.shields.io/badge/agent-ready-green" alt="Agent Status">
  </a>
  <img src="https://img.shields.io/badge/python-3.12-blue" alt="Python 3.12">
  <img src="https://img.shields.io/badge/framework-bindu-purple" alt="Bindu Framework">
  <img src="https://img.shields.io/badge/license-MIT-lightgrey" alt="MIT License">
</p>

## 🎯 What This Agent Does

Your **competitor-analysis-agent** is a sophisticated AI agent that:

*   **Automatically discovers competitors** for any company using web search
*   **Scrapes and analyzes competitor websites** using Firecrawl
*   **Generates comprehensive competitive intelligence reports** with:
    *   SWOT analysis for each competitor
    *   Feature comparison matrices
    *   Pricing analysis
    *   Market positioning insights
    *   Strategic recommendations

---

## Skills
The agent includes the `competitor-analysis` skill for comprehensive competitive intelligence:
- **Primary Capability**: Comprehensive competitive intelligence and market research
- **Features**: Web search for competitor discovery, website scraping for detailed information extraction, SWOT analysis and strategic recommendations
- **Limitations**: Requires API keys for web services; limited to publicly accessible content

- **Secondary Capability**: Strategic reporting and actionable insights generation (planned for v2.0.0)

---

## 🚀 Quick Start (Local Development)

### 1. Clone & Setup

```bash
git clone https://github.com/Paraschamoli/competitor-analysis-agent.git
cd competitor-analysis-agent
uv venv --python 3.12
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
uv sync
```

### 2. Configure API Keys

```bash
# Copy environment template
cp .env.example .env

# Edit .env and add your keys:
# FIRECRAWL_API_KEY (required) - from https://firecrawl.dev
# OPENAI_API_KEY or OPENROUTER_API_KEY (required for LLM)
# MEM0_API_KEY (optional) - for memory operations
```

### 3. Run the Agent

```bash
# Start the agent server
uv run python -m competitor_analysis_agent

# Agent runs on http://localhost:3773
```

### 4. Test with Sample Query

```bash
# Use curl or your preferred tool to test
curl -X POST http://localhost:3773/a2a \
  -H "Content-Type: application/json" \
  -d '{
    "messages": [
      {"role": "user", "content": "Analyze competitors for Notion and provide a competitive analysis report"}
    ]
  }'
```

---

## 🐳 Docker Deployment (Recommended)

### Using Docker Compose

```bash
# Start with Docker Compose (auto-builds from Dockerfile.agent)
docker-compose up --build

# Or run in background
docker-compose up -d
```

### Manual Docker Build

```bash
# Build the agent image
docker build -t competitor-analysis-agent -f Dockerfile.agent .

# Run the container
docker run -p 3773:3773 \
  -e FIRECRAWL_API_KEY=your_key \
  -e OPENROUTER_API_KEY=your_key \
  competitor-analysis-agent
```

---

## 🔧 Configuration Files

### agent_config.json - Core Agent Configuration

```json
{
  "name": "competitor-analysis-agent",
  "description": "AI Competitive Intelligence Agent",
  "version": "1.0.0",
  "deployment": {
    "url": "http://0.0.0.0:3773",
    "expose": true
  },
  "environment_variables": [
    {"key": "FIRECRAWL_API_KEY", "required": true},
    {"key": "OPENAI_API_KEY", "required": false},
    {"key": "OPENROUTER_API_KEY", "required": false},
    {"key": "MEM0_API_KEY", "required": false}
  ]
}
```

### pyproject.toml - Dependencies

Your agent uses:
*   **bindu (2026.1.7)** - Agent framework
*   **agno (≥2.2.0)** - Agent orchestration
*   **firecrawl-py** - Web scraping and search
*   **openai** - LLM integration
*   **mem0ai** - Memory management
*   **arxiv & pypdf** - Research paper analysis tools
*   **fastmcp** - Model Context Protocol tools

---

## 📊 Agent Workflow

Your agent follows this intelligent five-phase workflow:

1.  **Phase 1: Initial Research & Discovery**
    *   Searches for target company information
    *   Identifies competitors using web search
    *   Maps the competitive landscape

2.  **Phase 2: Competitor Website Analysis**
    *   Scrapes competitor websites using Firecrawl
    *   Extracts product information, pricing, features
    *   Analyzes site structure and user experience

3.  **Phase 3: Deep Analysis**
    *   Performs SWOT analysis for each competitor
    *   Creates feature comparison matrices
    *   Analyzes market positioning and pricing strategies

4.  **Phase 4: Strategic Synthesis**
    *   Generates strategic recommendations
    *   Identifies market opportunities and threats
    *   Provides actionable insights

5.  **Phase 5: Research Integration**
    *   Analyzes relevant research papers using Arxiv tools
    *   Incorporates academic insights into competitive analysis
    *   Uses memory tools for context-aware analysis

---

## 🎨 Usage Examples

### Via JSON-RPC API

```bash
curl --location 'http://localhost:3773' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer sk-or-v1-...' \
--data '{
  "jsonrpc": "2.0",
  "method": "message/send",
  "params": {
    "message": {
      "role": "user",
      "parts": [
        {
          "kind": "text",
          "text": "Analyze the competitive landscape for Slack. Identify top 3 competitors and analyze their features."
        }
      ],
      "kind": "message",
      "messageId": "990e8400-e29b-41d4-a716-446655440401",
      "contextId": "990e8400-e29b-41d4-a716-446655440402",
      "taskId": "990e8400-e29b-41d4-a716-446655440489"
    },
    "configuration": {
      "acceptedOutputModes": [
        "application/json"
      ]
    }
  },
  "id": "990e8400-e29b-41d4-a716-446655440404"
}'
```

### Sample Competitor Analysis Queries

- "Analyze the competitive landscape for Stripe in the payments industry"
- "Research competitors to Shopify in the e-commerce platform market"
- "Conduct a competitive analysis of Zoom in the video conferencing space"
- "Compare Salesforce with its main competitors in the CRM market"
- "Analyze market positioning of Tesla versus other EV manufacturers"
- "Research direct and indirect competitors for Netflix"
- "Perform SWOT analysis on Apple's main competitors in smartphone market"

---

## 📁 Project Structure

```text
competitor-analysis-agent/
├── competitor_analysis_agent/          # Main agent package
│   ├── __init__.py                     # Public API exports
│   ├── main.py                         # Main agent implementation
│   ├── agent_config.json               # Agent configuration
│   └── skills/                         # Agent skills
│       └── competitor-analysis/        # Skill implementation
│           └── skill.yaml              # Skill configuration
├── Dockerfile.agent                    # Multi-stage Docker build
├── docker-compose.yml                  # Docker orchestration
├── pyproject.toml                      # Python dependencies
├── uv.lock                             # Dependency lock file
├── .env.example                        # Environment template
├── .github/workflows/                  # CI/CD workflows
│   └── build-and-push.yml              # Docker build and push
├── tests/                              # Test files
│   └── test_main.py                    # Agent tests
└── README.md                           # This file
```

## 🔌 API Reference

### Health Check

```bash
GET http://localhost:3773/health
```

Response:
```json
{"status": "healthy", "agent": "Competitor Analysis Agent"}
```

### Chat Endpoint

```bash
POST http://localhost:3773/chat
Content-Type: application/json

{
  "messages": [
    {"role": "user", "content": "Your competitor analysis query here"}
  ]
}
```

## 🧪 Testing

### Local Testing

```bash
# Install test dependencies
uv sync --group dev

# Run tests
pytest tests/

# Test with specific API keys
FIRECRAWL_API_KEY=test_key python -m pytest
```

### Integration Test

```bash
# Start agent
python competitor_analysis_agent/main.py &

# Test API endpoint
curl -X POST http://localhost:3773/chat \
  -H "Content-Type: application/json" \
  -d '{"messages": [{"role": "user", "content": "Analyze competitors for Trello"}]}'
```

### Key Implementation Details
Your agent (`competitor_analysis_agent/main.py`) features:
*   **Model Selection Logic:** Automatically chooses between OpenAI and OpenRouter
*   **Firecrawl Integration:** Web scraping and search capabilities
*   **Reasoning Tools:** Built-in analysis and critical thinking
*   **Lazy Initialization:** Optimized resource usage
*   **Comprehensive Instructions:** Detailed five-phase analysis workflow
*   **MCP Tools Support:** Model Context Protocol integration
*   **Memory Management:** Mem0 integration for context-aware analysis
*   **Research Capabilities:** Arxiv tools for academic research integration

---

## 🔑 Required API Keys

### 1. FIRECRAWL_API_KEY (Required)
*   Get from: [firecrawl.dev](https://firecrawl.dev)
*   Used for web scraping and search functionality
*   Essential for competitor website analysis

### 2. LLM Provider (Choose One)
*   **OPENAI_API_KEY:** For GPT-4o access (from OpenAI)
*   **OPENROUTER_API_KEY:** Alternative LLM provider (from OpenRouter)

### 3. MEM0_API_KEY (Optional)
*   For memory and context management
*   Get from: [app.mem0.ai](https://app.mem0.ai)

---

## � Dependencies

### Core Packages
*   **bindu** - Agent deployment framework
*   **agno** - AI agent framework
*   **firecrawl-py** - Web scraping and search
*   **openai** - OpenAI client
*   **requests** - HTTP requests
*   **rich** - Console output
*   **python-dotenv** - Environment management

### Development Packages
*   **pytest** - Testing framework
*   **ruff** - Code formatting/linting
*   **pre-commit** - Git hooks
uv run pytest

# Format code
uv run ruff format .

# Lint code
uv run ruff check --fix .

# Run agent directly
uv run python -m competitor_analysis_agent

# Run pre-commit checks
uv run pre-commit run --all-files
```

---

## 📈 Output Format

The agent generates structured reports including:

```markdown
# Competitive Analysis Report: {Company}

## Executive Summary
{High-level overview}

## Research Methodology
- Search queries used
- Websites analyzed
- Research papers reviewed

## Competitor Analysis
### Competitor 1: {Name}
- SWOT Analysis
- Products & Services
- Pricing Analysis
- Market Positioning

## Comparative Analysis
- Feature Comparison Matrix
- Pricing Comparison Table
- Market Positioning Map

## Strategic Insights
- Key findings with evidence
- Competitive advantages
- Market risks and challenges

## Strategic Recommendations
- Immediate Actions (0-3 months)
- Short-term Strategy (3-12 months)
- Long-term Strategy (12+ months)
```

---

## 🌐 Deploy to bindus.directory

Make your agent discoverable worldwide:

```bash
# 1. Get Bindu API token from bindus.directory
# 2. Configure GitHub Secrets:
gh secret set BINDU_API_TOKEN --body "your_token"
gh secret set DOCKERHUB_TOKEN --body "your_docker_token"

# 3. Push to trigger auto-deployment
git push origin main
```

**Auto-deployment features:**
*   Automatic Docker image building
*   Multi-architecture support (linux/amd64, linux/arm64)
*   Registration on bindus.directory
*   Version tagging and caching

---

## 🔍 Testing the Agent

### Test Query via API
```bash
# Test the running agent (use /a2a endpoint)
curl -X POST http://localhost:3773/a2a \
  -H "Content-Type: application/json" \
  -d '{
    "messages": [
      {"role": "user", "content": "Analyze competitors for Trello"}
    ]
  }'
```

### Check Agent Health
```bash
# Verify agent is running
curl http://localhost:3773/health

# Check deployment status
curl http://localhost:3773/deployment

# Get agent information
curl http://localhost:3773/agent/info
```

### View API Documentation
Open your browser to `http://localhost:3773/docs` for interactive API documentation.

---

## 🚨 Troubleshooting

**Common Issues:**

1.  **"FIRECRAWL_API_KEY is required"**
    *   Get a key from [firecrawl.dev](https://firecrawl.dev)
    *   Add to `.env` file

2.  **Agent fails to initialize**
    *   Check Python version (requires 3.12+)
    *   Verify all dependencies with `uv sync`
    *   Check API keys in `.env` file

3.  **Docker build fails**
    *   Ensure Docker daemon is running
    *   Check `Dockerfile.agent` syntax
    *   Verify Docker Hub credentials

4.  **No LLM API key provided**
    *   Agent can start without LLM key, but will fail at runtime when LLM is needed
    *   Add either OpenAI or OpenRouter key

5.  **Permission errors on Windows**
    *   Run terminal as administrator
    *   Check file permissions for `agent_config.json`

6.  **Pre-commit hooks failing**
    *   Install required dev dependencies: `uv sync --group dev`
    *   Run `uv run pre-commit install` to install hooks
    *   Fix formatting issues with `uv run ruff format .`

---

## 📝 License

MIT License - See LICENSE file for details.

## 🤝 Contributing

Contributions welcome! Please follow these steps:

1.  Fork the repository
2.  Create a feature branch: `git checkout -b feature/improvement`
3.  Make your changes following the code style
4.  Add tests for new functionality
5.  Commit with descriptive messages
6.  Push to your fork
7.  Open a Pull Request

**Code Style:**
*   Follow PEP 8 conventions
*   Use type hints where possible
*   Add docstrings for public functions
*   Keep functions focused and small

## 🙏 Credits & Acknowledgments

*   **Developer:** Paras Chamoli
*   **Framework:** Bindu - Agent deployment platform
*   **Agent Framework:** Agno - AI agent toolkit
*   **Web Intelligence:** Firecrawl - Advanced web scraping
*   **Reasoning Tools:** Agno ReasoningTools for critical analysis

## 🔗 Useful Links

*   🌐 **Bindu Directory:** [bindus.directory](https://bindus.directory)
*   📚 **Bindu Docs:** [docs.getbindu.com](https://docs.getbindu.com)
*   🐙 **GitHub:** [github.com/ParasChamoli/competitor-analysis-agent](https://github.com/ParasChamoli/competitor-analysis-agent)
*   💬 **Discord:** Bindu Community

<br/>

<p align="center">
  <strong>Built with ❤️ by Paras Chamoli</strong><br/>
  <em>Transforming competitive research with AI-powered analysis</em>
</p>

<p align="center">
  <a href="https://github.com/ParasChamoli/competitor-analysis-agent/stargazers">⭐ Star on GitHub</a> •
  <a href="https://bindus.directory">🌐 Register on Bindu</a> •
  <a href="https://github.com/ParasChamoli/competitor-analysis-agent/issues">🐛 Report Issues</a>
</p>

---
