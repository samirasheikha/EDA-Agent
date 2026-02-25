## Good Prompts properties
-Do: 


Role definition – Who is the AI acting as? ("You are a customer support assistant...")
Goal specification – What should it do? ("Answer questions about product pricing and features...")
Instructions and constraints – Any do’s and don’ts? ("Keep responses under 200 words, avoid technical jargon...")


-Don't:


Examples – Don’t provide sample inputs and expected outputs as this is already covered in the input and output arguments.


LLMs don’t think. They follow instructions—precisely. Ambiguity confuses them. Over-explaining can be just as bad as under-explaining. And remember: LLMs will generate an answer, even if it’s wrong. You have to manage this risk. (https://www.freecodecamp.org/news/how-to-write-effective-prompts-for-ai-agents-using-langbase/)


A system prompt can even be 1000s lines (like https://app.prompthub.us/prompthub/cline-system-prompt)! So there are two ways to add them into an agent, which are in the agent or add from a  text file. Also, for long prompts, you can split different parts of it to differents txt files like tools, instructions, examples, and then add them into the agent code respectively. (for more, see next )





