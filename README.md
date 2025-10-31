**Course (Long-Term Agentic Memory With LangGraph)**



why --> because it is very important to make model learn about past events, preferences, and facts — especially for assistant-type agents — so that they give more efficient and contextually aware results.
In simple terms, memory helps an AI agent remember user interactions, understand long-term context, and provide more human-like, personalized responses over time.



how --> to add memory we must know what to store, when to store it, and what to retrieve later.
For example, if a user says “My friend Ali’s birthday is on 5th March,” the agent should store this as a fact and later recall it when asked, “When is Ali’s birthday?”



To add memory, we use the langmem library to manage different types of memory efficiently.
It also supports vector databases, which make it possible to search through stored information — such as past user inputs or relevant facts — using similarity search techniques.



How agents interact with memory





Hot Path



Definition: Immediately updates memory alongside user prompts — everything happens in one go, during the same conversation.

Example: When you tell an assistant, “My favorite color is blue,” and it instantly remembers that fact for the next message.

Implementation: Done by a single agent that updates its memory synchronously as it interacts.




Background Paradigm



Definition: Updates memory at the end of the conversation — after a delay, such as a few minutes or once the interaction session is complete.

Example: After finishing a chat, the system reviews the dialogue, extracts key facts, and stores them for future use.

Benefit: Reduces processing load during active interactions and allows post-analysis or filtering of what should be remembered.







<img width="1110" height="232" alt="image" src="https://github.com/user-attachments/assets/683035a3-4f38-4139-9aed-0fbce1c259ab" />






Types of Memory

Semantic Memory

What it stores: Facts, numbers, and static information (e.g., birthdays, names, definitions).

Purpose: To help the agent recall factual data quickly and accurately.

Example: “Ali’s birthday is on 5th March.”





Episodic Memory





What it stores: Experiences and past agent actions — basically what has happened before.

Purpose: To help the agent recall previous interactions or context of past tasks.

Example: Remembering that last time the user asked for an email draft or a weather update.





Procedural Memory

What it stores: Instructions, skills, or procedures the agent must follow to complete a task.

Purpose: To maintain consistency in task execution.

Example: Remembering how to send an email or which tools to use for sentiment analysis.




Implemented Email Assistant







<img width="572" height="255" alt="image" src="https://github.com/user-attachments/assets/77801909-cb04-4dfe-83ee-6885547b5440" />







First Implementation (Semantic Memory)

Ask: “Ali is my friend.”

Then test: “Who is my friend?”

The agent retrieves the stored fact from semantic memory and replies correctly.





Second Implementation (Semantic Memory + Feedback)

Similar setup as before but now includes a feedback mechanism.

If the model gives an incorrect or incomplete answer, user feedback helps update or refine the stored memory — improving accuracy over time.






Third Implementation (Procedural Memory)

The agent is given prompts or instructions on which tools to pick and when during execution.

This allows the assistant to make better decisions on its own while performing tasks (e.g., deciding whether to use the “email search” tool or “compose email” tool).
