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


Implemented langGraph Components 

Q:Persistance
ability to save and maintain state over time. Go back and resume in particular state in langGraph and to implement in LangGraph we use check-pointer

Q:Streaming

ability to provide real-time updates while the graph is executing, rather than only providing a final result at the end

Q:Async Methods

While one task waits e.g, for an API response , another task can keep running.

LangChain Online Resources

Q:Multi-agent System vs Supervisor

In multi-agent several agents work together to achieve a goal while in supervisor we a powerful agent that supervises other agents

