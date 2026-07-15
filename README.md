# Claude with the Anthropic API

A hands-on collection of focused notebooks exploring the **Anthropic API** and the
**Claude Messages API**, built while completing Anthropic Academy's
[*Building with the Claude API*](https://anthropic.skilljar.com/claude-with-the-anthropic-api)
course. Each notebook is small and self-contained, and demonstrates one capability of
the API — from basic requests to system prompts, streaming, and output control.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic-Claude_API-D97757?logo=anthropic&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

## What's inside

| # | Notebook | Demonstrates | API feature / concept |
| --- | --- | --- | --- |
| 001 | [`001_requests.ipynb`](001_requests.ipynb) | Building a multi-turn conversation and a simple chat loop | Messages API · `messages.create` |
| 002 | [`002_system_prompt.ipynb`](002_system_prompt.ipynb) | Steering Claude's role and behavior with a system prompt | `system` parameter |
| 003 | [`003_temperature.ipynb`](003_temperature.ipynb) | Controlling how deterministic vs. creative responses are | `temperature` parameter |
| 004 | [`004_streaming.ipynb`](004_streaming.ipynb) | Receiving tokens incrementally as they are generated | `stream=True` · `messages.stream` |
| 005 | [`005_controlling_output.ipynb`](005_controlling_output.ipynb) | Cutting generation short at a marker | `stop_sequences` parameter |
| 006 | [`006_prompt_evals.ipynb`](006_prompt_evals.ipynb) | Building an eval loop: generate a dataset, run prompts, grade with an LLM judge and syntax checks | Prompt evaluation · model grading + code validation |
| 007 | [`007_prompting.ipynb`](007_prompting.ipynb) | Structured prompt design — role, guidelines, XML-tagged inputs, and a few-shot example — evaluated end to end | Prompt engineering · eval loop |
| 008 | [`008_prompting_exercise.ipynb`](008_prompting_exercise.ipynb) | Applying the eval workflow to a topic-extraction task graded on JSON-shape criteria | Prompt engineering · exercise |
| 009 | [`009_tools.ipynb`](009_tools.ipynb) | Defining custom tools and running the agentic loop — parallel calls, matched `tool_result` blocks, `is_error` recovery | Tool use · `tools` · `stop_reason: "tool_use"` |
| 010 | [`010_tool_streaming.ipynb`](010_tool_streaming.ipynb) | Streaming tool calls and watching tool inputs arrive fragment by fragment | Fine-grained tool streaming · `eager_input_streaming` |
| 011 | [`011_text_editor_tool.ipynb`](011_text_editor_tool.ipynb) | Implementing the Anthropic-defined text editor tool client-side, with path sandboxing and backups | `text_editor_20250728` · client tools |
| 012 | [`012_web_search.ipynb`](012_web_search.ipynb) | Letting Claude search the web and answer with cited sources | `web_search_20260318` · server tools |
| 013 | [`013_chunking.ipynb`](013_chunking.ipynb) | Comparing chunking strategies — by characters, sentences, and document sections | RAG · text chunking |
| 014 | [`014_embeddings.ipynb`](014_embeddings.ipynb) | Generating text embeddings and ranking chunks by cosine similarity | Voyage AI · `voyage-4` · `input_type` |
| 015 | [`015_vectordb.ipynb`](015_vectordb.ipynb) | Building an in-memory vector database with brute-force cosine search | RAG · semantic search |
| 016 | [`016_bm25.ipynb`](016_bm25.ipynb) | Implementing BM25 lexical search from scratch — TF, IDF, and length normalization | RAG · keyword search |
| 017 | [`017_hybrid.ipynb`](017_hybrid.ipynb) | Merging semantic and lexical rankings with Reciprocal Rank Fusion | RAG · hybrid search · RRF |

Each notebook reuses a small set of helpers (`add_user_message`,
`add_assistant_message`, `chat`) so the focus stays on the one feature it introduces.

## Course roadmap

The course spans API fundamentals through agentic workflows. This repository grows as I
progress — completed topics are checked off, upcoming ones are listed so the plan is
visible.

- [x] **API fundamentals** — requests, system prompts, temperature, streaming, output control (`001`–`005`)
- [x] **Prompt engineering & evaluation** — writing, testing, and grading prompts (`006`–`008`)
- [x] **Tool use** — letting Claude call external functions and tools (`009`–`012`)
- [x] **Retrieval (RAG)** — chunking, embeddings, vector search, BM25, and hybrid retrieval (`013`–`017`)
- [ ] **Agentic workflows** — chaining, parallelization, and routing patterns

## Setup

```bash
# 1. Clone and enter the repository
git clone https://github.com/JuanCamiloMendoza99/claude-anthropic-api.git
cd claude-anthropic-api

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add your API keys
cp .env.example .env            # then edit .env and paste your keys
```

Get an Anthropic API key at <https://console.anthropic.com/settings/keys>. The RAG
notebooks (`013`+) also use a [Voyage AI](https://dashboard.voyageai.com/) key for
embeddings, since Anthropic recommends Voyage as its embeddings provider.

## Running the notebooks

Launch Jupyter and open any notebook, then run the cells top to bottom:

```bash
jupyter lab        # or: jupyter notebook
```

Each notebook loads your key from `.env` automatically via `python-dotenv`, so no key
ever appears in the code.

## Skills demonstrated

- Anthropic **Messages API** — single requests and multi-turn conversations
- **System prompts** to shape Claude's role, tone, and constraints
- **Sampling controls** with the `temperature` parameter
- **Streaming** responses token by token, including inspecting raw stream events
- **Output control** with `stop_sequences`
- **Prompt evaluation** — generating a test dataset and scoring prompt outputs with both an
  LLM-as-judge and programmatic syntax validation (JSON, Python, regex)
- **Tool use** — defining custom tools with JSON Schemas and running the agentic loop:
  executing parallel tool calls, returning matched `tool_result` blocks, and reporting
  failures with `is_error` so Claude can recover
- **Tool streaming** — fine-grained input streaming (`eager_input_streaming`) to receive
  large tool arguments incrementally as Claude generates them
- **Anthropic-defined client tools** — a `text_editor_20250728` implementation with
  directory-sandboxed path validation and pre-edit backups
- **Server tools** — web search with domain-use caps, response block inspection, and
  cited sources
- **Retrieval (RAG) building blocks** — chunking strategies (character, sentence, and
  section-based); **Voyage AI embeddings** (`voyage-4`) with retrieval-tuned
  `input_type` prompts for documents vs. queries and batched requests; a from-scratch
  in-memory **vector index** (cosine distance); **BM25** lexical scoring; and
  **hybrid search** that fuses both rankings with Reciprocal Rank Fusion
- Practical hygiene: environment-based secrets (`python-dotenv`), a clean
  `.gitignore`, pinned dependencies, and readable, reusable helper functions

## Author

**Juan Camilo Mendoza** · [GitHub](https://github.com/JuanCamiloMendoza99)
