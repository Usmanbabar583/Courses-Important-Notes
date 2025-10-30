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

Each agent handles its specific domain (e.g., one for planning, one for writing, one for checking).
They communicate through a shared state or messages, allowing distributed problem-solving.
Example:

Planner Agent → divides the task

Research Agent → gathers info

Writer Agent → generates the report





Implement a simple ReAct Agent using llm and Python (Thought → Action → Observation → Thought → … → Final Answer)


<img width="246" height="177" alt="image" src="https://github.com/user-attachments/assets/7c647246-3827-40a4-94e9-b495e98005f3" />




The ReAct (Reasoning + Acting) pattern combines logical thinking with action-taking.
An agent reasons about what to do next “Thought”, takes an action “Action”, observes the result (“Observation”), and continues this loop until it reaches the final answer.

Example Workflow:


Thought: I need to know the current weather.


Action: Use weather_api tool.


Observation: It’s 25°C and sunny.


Thought: Now I can tell the user it’s a nice day.


Final Answer: “It’s sunny and 25°C today.”




Components of a LangGraph


1-Prompt Tempelates


Templates define the structure and context for LLM inputs.




Graph Structure


<img width="541" height="355" alt="image" src="https://github.com/user-attachments/assets/e33bf556-88b6-4506-959c-0509308968cf" />





2-Tools (functions to extend capability of an agent - APIS, web_search)


Tools are external functions or APIs that enhance the agent’s power.
They allow integration with databases, web search, or custom logic.
LangGraph connects tools as nodes or within agent functions for flexible workflows.




3-Nodes (functions or agents - representing a step)


Each node in LangGraph represents a single operation — a reasoning step, a tool call, or even another agent.
Nodes can be synchronous or asynchronous and are connected through edges.



4-Edges (connections between nodes)


Edges represent the flow of data or logic between nodes.
They determine which node runs next after the current one finishes execution.




5-Conditional Edges (decide what to do if condition fullfilled)

Conditional edges allow branching decisions — different paths depending on outcomes.
Example:
If the tool’s output contains “error,” go to an error-handling node; otherwise, proceed normally.




6-State (Representing Current Context or data - accessable to all nodes)


State holds the agent’s current context — like conversation history, tool outputs, or variable values.
All nodes can access and update this shared state, making it easy to pass data throughout the workflow.



Implemented langGraph Components 


class Agent:

    def __init__(self, model, tools, system=""):
        self.system = system
        graph = StateGraph(AgentState)
        graph.add_node("llm", self.call_openai)
        graph.add_node("action", self.take_action)
        graph.add_conditional_edges(
            "llm",
            self.exists_action,
            {True: "action", False: END}
        )
        graph.add_edge("action", "llm")
        graph.set_entry_point("llm")
        self.graph = graph.compile()
        self.tools = {t.name: t for t in tools}
        self.model = model.bind_tools(tools)

    def exists_action(self, state: AgentState):
        result = state['messages'][-1]
        return len(result.tool_calls) > 0

    def call_openai(self, state: AgentState):
        messages = state['messages']
        if self.system:
            messages = [SystemMessage(content=self.system)] + messages
        message = self.model.invoke(messages)
        return {'messages': [message]}

    def take_action(self, state: AgentState):
        tool_calls = state['messages'][-1].tool_calls
        results = []
        for t in tool_calls:
            print(f"Calling: {t}")
            if not t['name'] in self.tools:      # check for bad tool name from LLM
                print("\n ....bad tool name....")
                result = "bad tool name, retry"  # instruct LLM to retry if bad
            else:
                result = self.tools[t['name']].invoke(t['args'])
            results.append(ToolMessage(tool_call_id=t['id'], name=t['name'], content=str(result)))
        print("Back to the model!")
        return {'messages': results}





Q:Persistance
ability to save and maintain state over time. Go back and resume in particular state in langGraph and to implement in LangGraph we use check-pointer.
In LangGraph, persistence ensures that the workflow’s state can be saved, paused, and resumed later. 
It is especially useful for long-running tasks or human-in-the-loop workflows. 
The checkpointer acts like a memory snapshot — storing the current graph state so it can continue later from the same point.



Q:Streaming

ability to provide real-time updates while the graph is executing, rather than only providing a final result at the end. Streaming allows the agent to send partial or live updates as it works.
Instead of waiting for the entire response, the system streams intermediate outputs (like token-by-token text or step-by-step progress).
This improves user experience, especially in chat interfaces where you can see the model’s output appearing in real-time.



Q:Async Methods

While one task waits e.g, for an API response , another task can keep running. Asynchronous methods (async/await in Python) let LangGraph run multiple operations concurrently.
This is crucial when agents call APIs, run long processes, or handle multiple nodes simultaneously.
It prevents blocking and ensures faster, smoother performance.



LangChain Online Resources


LangChain provides comprehensive documentation, tutorials, and guides for learning LangGraph, ReAct agents, and multi-agent coordination.




Q:Multi-agent System vs Supervisor

In multi-agent several agents work together to achieve a goal while in supervisor we a powerful agent that supervises other agents



In multi-agent several agents work together to achieve a goal while in supervisor we a powerful agent that supervises other agents

In a Multi-Agent System, each agent operates autonomously with its own role and logic. They collaborate and exchange results to complete a task collectively.
Example: One agent collects data, another analyzes it, and a third summarizes findings.

In a Supervisor System, one central (supervisor) agent manages and controls other agents. It decides which agent should act next, monitors their outputs, and ensures the overall workflow stays consistent.
Example: The supervisor reviews the task and instructs either the “DataAgent” or “WriterAgent” depending on the stage.


<img width="912" height="538" alt="image" src="https://github.com/user-attachments/assets/e44edfc0-6606-43b4-be1f-3afe0e96710f" />






<img width="735" height="533" alt="image" src="https://github.com/user-attachments/assets/295bbad4-7f47-47f5-800c-f01bf160928b" />

