+++
title = "LLM powered Research assistant"
date = 2025-01-10
updated = 2025-01-10
description = "How to build a research assistant powered by LLM."

[taxonomies]
tags = ["NLP",
        "Automation"]
+++

<!-- title: "LLM powered Research assistant" -->
<!-- date: "2025-01-10" -->
<!-- description: "In this article, I explore how to build a research assistant powered by LLM." -->
<!-- categories : -->
<!--     - "Computer Engineering" -->
<!-- tags: -->
<!--     - "AI" -->
<!--     - "Research" -->
<!--     - "Assistant" -->
<!--     - "NLP" -->
<!--     - "Automation" -->

# Abstract

Natural Language Processing (NLP) has been a hot topic in the field of
Artificial Intelligence (AI) for the past few years. The advancement in
transformer models has made it easier to build powerful NLP models.
Furthermore, better hardware and software tools have made it easier to take
advantage of these models for much broader applications. In this article, I
explore the pros and cons of LLM agents, different design architectures, and
how to build a research assistant powered by LLM.

# Introduction

In this article, the core concept is to evaluate the potential of using LLM
as a cog in the wheel of automation. Web crawling, data extraction, and
summarization are some of the tasks that was traditionally hard to automate
due to the complexity of the natural language. Meanwhile, the world wide web
in this era is crowded with misinformation and biased information. Considering
the fact that manual web surfing is time consuming and error prone, it is
imperative to automate the process of information extraction and summarization.

# Related Works

There is no shortage of research on NLP and LLM. The most popular LLM models
are GPT-4o, ollama, Claude 3.5 Sonnet, and Gemini. The founders of these
models have published numerous papers and articles on the topic. The said
companies are mainly focused on on improving the and expanding the LLM models
or building frameworks and tools to make it easier to build applications on
top of these models.

# Problem Statement

An LLM by itself can not achieve much. To improve it for the purpose of
automation, we can make use of a framework that can help us to build a
research assistant. The research assistant should be able to crawl the web,
extract information, summarize it, and present it in a readable format. The
research assistant should also be able to answer questions based on the
information it has extracted.

# Materials and Methods

The research assistant is built using Python. The core libraries used are
Langgraph, and the libraries in its ecosystem.

## Concepts and Glossary

- Graph: in Langgraph framework, a graph is the representation of flow of
  information. It is a directed graph where nodes are the tasks and edges are
  the dependencies between the tasks.
- Agent: the agent is the entity that performs the tasks. It is the LLM model
  in this case.
- Tools: the functions with a clear input and output. The agent makes use of
  these tools to perform the tasks.
- Embedding models: it's a model that converts and represents the text in a
  vector space. Currently, most popular embedding models are transformer based.
- Vector store: it's a storage that stores the embeddings of the text. It helps
  to reduce the computation time.

## Design Architecture

There are many different ways to design the architecture of the research
assistant. The most powerful and flexible way is to use a graph based framework
for Chain-of-Thought (CoT) reasoning. A Retrieval-Augmented generation to
enhance the generation of the text with more reliable information. Tool-use
Agents to provide the tools for an adaptive agent to use. And a
Memory-Augmented Transformer to store the information for future use.

The two main design architectures that i exprimented with and found to be
effective are:

1. **Master-Slave Architecture**: In this architecture, the master agent
   controls the slave agents. The master agent is responsible for the
   high-level tasks like managing the flow of information, storing and
   retrieving chat history, and answering questions. The slave agents are
    responsible for the low-level tasks like crawling the web, extracting
    information, summarizing it, and presenting it in a readable format.

{% mermaid() %}
graph TD;
        __start__([<p>__start__</p>]):::first
        master_agent(master_agent)
        rag_search_filter(rag_search_filter)
        rag_search(rag_search)
        fetch_arxiv(fetch_arxiv)
        web_search(web_search)
        final_answer(final_answer)
        __end__([<p>__end__</p>]):::last

        __start__ --> master_agent
        rag_search_filter --> master_agent
        rag_search --> master_agent
        fetch_arxiv --> master_agent
        web_search --> master_agent
        final_answer --> __end__

        master_agent -.-> rag_search_filter
        master_agent -.-> rag_search
        master_agent -.-> fetch_arxiv
        master_agent -.-> web_search
        master_agent -.-> final_answer
        master_agent -.-> __end__

        classDef default fill:#f2f0ff,line-height:1.2
        classDef first fill-opacity:0
        classDef last fill:#bfb6fc
{% end %}

2. **Flow-Based Architecture**: In this architecture, the flow of information
   is represented as a directed graph. Each node in the graph is a task, and
   each edge is a dependency between the tasks. The agent starts at the
   starting node and follows the edges to perform the tasks. The agent can
   also backtrack if it gets stuck at a task or needs to redo a task. In this
   example, the emphasis is on self-reflective nature of implementation.

{% mermaid() %}
graph TD;
        __start__([<p>__start__</p>]):::first
        generic_chat(generic_chat)
        embed_uploaded_document(embed_uploaded_document)
        generate_query(generate_query)
        web_research(web_research)
        summarize_sources(summarize_sources)
        reflect_on_summary(reflect_on_summary)
        finalize_summary(finalize_summary)
        __end__([<p>__end__</p>]):::last

        embed_uploaded_document --> web_research;
        finalize_summary --> __end__;
        generate_query --> embed_uploaded_document;
        generic_chat --> __end__;
        summarize_sources --> reflect_on_summary;
        web_research --> summarize_sources;

        __start__ -.-> generate_query;
        __start__ -.-> generic_chat;
        reflect_on_summary -.-> finalize_summary;
        reflect_on_summary -.-> web_research;

        classDef default fill:#f2f0ff,line-height:1.2
        classDef first fill-opacity:0
        classDef last fill:#bfb6fc
{% end %}

## Implementation

The information that flow through the graph is represented as a state and can
hold many different key values.

```python
@dataclass(kw_only=True)
class SummaryState:
    research_topic: str = field(default=None)  # Report topic
    search_query: str = field(default=None)  # Search query
    web_research_results: Annotated[list, operator.add] = field(default_factory=list)
    sources_gathered: Annotated[list, operator.add] = field(default_factory=list)
    research_loop_count: int = field(default=0)  # Research loop count
    running_summary: str = field(default=None)  # Final report
```

The system and human prompt for each agent should be clear and concise.
Additionall information can be formatted dynamically to the prompt.

```python
"""
here is the previous chat history:
{chat_history}
"""
```

It's also noteworthy that with cerful prompt design, the agent can be used
to return information used for conditional logic.

The next key step is to define the tools and binding them to the agent.

```python
model = load_chat_model(configuration.model)

tools=[
    web_search,
    rag_search,
]

model.bind_tools(tools)
```

Finally, the `StateGraph` class is used to define the flow of information.
by binding the nodes and edges to the agent.

```python

builder = StateGraph(SummaryState, input=SummaryStateInput, output=SummaryStateOutput, config_schema=Configuration)
builder.add_node("generic_chat", generic_chat)
builder.add_node("embed_uploaded_document", embed_uploaded_document)
builder.add_node("generate_query", generate_query)
builder.add_node("web_research", web_research)
builder.add_node("summarize_sources", summarize_sources)
builder.add_node("reflect_on_summary", reflect_on_summary)
builder.add_node("finalize_summary", finalize_summary)

# Add edges
builder.add_conditional_edges(START, check_user_input)
builder.add_edge("generate_query", "embed_uploaded_document")
builder.add_edge("embed_uploaded_document", "web_research")
builder.add_edge("web_research", "summarize_sources")
builder.add_edge("summarize_sources", "reflect_on_summary")
builder.add_conditional_edges("reflect_on_summary", route_research)
builder.add_edge("finalize_summary", END)
builder.add_edge("generic_chat", END)
```

# Evaluation

Evaluation an output of LLM, normally done with a set of predefined inputs and
outputs. The generated output is compared with the expected output. Comparing
is done using a cosine similarity or ROUGE score. However, for task such as
this that, the output can widely vary, I did not possess a predefined output.
Instead, I used a pairwise evaluation technique to compare the output of this
model, a `llama-3.2-70b` and `GPT-4o`. The judgement was based on the quality of
the summary, the relevance of the information, and the readability of the
summary. The Judge was a GPT-4o model.

The results showed a significant improvement over the `llama-3.2-70b`. However,
In all the tests, the `GPT-4o` model outperformed the research assistant.

# Conclusion

The research assistant powered by LLM is a powerful tool that can be used to
automate the process of information extraction and summarization. The
research assistant can crawl the web, extract information, summarize it, and
present it in a readable format. This may enhance the lives of people who
depend on information on the web. But, this is not the only use case of the
agentic models. This can help automate systems that previously required human
labor for a small portion of the flow. This system can introduce automation to
the systems that where not possible before, i.e. self-correcting systems that
required chain of thought reasoning.
