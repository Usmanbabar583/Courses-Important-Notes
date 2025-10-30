# Courses-Important-Notes
**Course (Long-Term Agentic Memory With LangGraph)**
Objective --> why and how to add memory in ai agents
why --> because it is very important to make model learn about past events, preferences,facts especially assistant agents so that they give more efficient results.
how --> to add memory we must know what to store and when and what to retrieve
to add memory we use **langmem** library to manage memory and it also supports vector database that provide searchable tools
**How agents interact with memory** 
1-> Hot Path (Immediately updates memory alongside user prompts -- in one go, it is done by single agent)
2-> Background paradigm (updates memory at the end of the conversion -- after some minutes)
**Types of Memory**
1-> Semantic Memory (stores facts,numbers e.g birthdays)
2-> Episodic Memory (stores experiences e.g past agent actions)
3-> Procedural Memory (stores intructions to follow provided to complete a task)
Implemented Email Assistant 
First Implement semantic memory in email assistant agent(by asking ali is my friend and ask response)
Second Implement semantic memory in email assistant agent(by asking ali is my friend and ask response and also require feedback)
third by giving prompts to pick particular tools when required (procedural)


**Course (AI Agents in LangGraph)**
Design Patterns to develop Agentic AI Workflows
Objective (How to build langchain agents using LangGraph)
1-Planning (how to complete a task step by step -- from outline to what to do after that)
2-Tools (what tools are available and when to use e.g search tool)
3-Reflection (thinking about own response and try to improve it)
4-Multi-Agent Collaboration (where multiple agents interact to achieve a specific goal)

Implement a simple ReAct Agent using llm and Python (Thought → Action → Observation → Thought → … → Final Answer)
Tmplement same agent using LangGraph
Components of a LangGraph
1-Prompt Tempelates
2-Tools (functions to extend capability of an agent - APIS, web_search)
3-Nodes (functions or agents - representing a step)
4-Edges (connections between nodes)
5-Conditional Edges (decide what to do if condition fullfilled)
6-State (Representing Current Context or data - accessable to all nodes)
