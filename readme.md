**Course (AI Agents in LangGraph)**


Objective--> (How to build langchain agents using LangGraph. The goal of this course is to understand how LangGraph can be used as an extension of LangChain to design, manage, and execute agentic AI workflows)

Design Patterns to develop Agentic AI Workflows

These patterns define the core behavior and thinking process of modern AI agents. Each design pattern represents approach to make the agents more autonomous and intelligent.


1-Planning (how to complete a task step by step -from outline to what to do after that)

The agent first creates an outline of the task (like a to-do list) and then decides the order in which to complete each part.
This makes the workflow structured and also help make agent organized.
For example,
Step 1: Understand the user’s question

Step 2: Search for relevant data

Step 3: Summarize and answer



2-Tools (what tools are available and when to use e.g search tool)

They let the agent take actions like searching the web, calling APIs, calculating values, or reading files.
The key is deciding when and which tool to use.
Example tools:

search_tool() – for web lookup

math_tool() – for performing calculations

api_tool() – for connecting with external systems



3-Reflection (thinking about own response and try to improve it)


Reflection is a process in which the agent reviews its previous answer, identifies mistakes or weak reasoning, and then improves the response.
This step helps the model self-correct and generate better answers over time.
For example, after giving an output, the agent might ask itself:

“Was my answer accurate and complete?”

If not, it revises the reasoning and tries again.




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

