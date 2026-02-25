## Good Prompts properties
-Do: 


Role definition – Who is the AI acting as? ("You are a customer support assistant...")
Goal specification – What should it do? ("Answer questions about product pricing and features...")
Instructions and constraints – Any do’s and don’ts? ("Keep responses under 200 words, avoid technical jargon...")


-Don't:


Examples – Don’t provide sample inputs and expected outputs as this is already covered in the input and output arguments.


LLMs don’t think. They follow instructions—precisely. Ambiguity confuses them. Over-explaining can be just as bad as under-explaining. And remember: LLMs will generate an answer, even if it’s wrong. You have to manage this risk. (https://www.freecodecamp.org/news/how-to-write-effective-prompts-for-ai-agents-using-langbase/)


A system prompt can even be 1000s lines (like https://app.prompthub.us/prompthub/cline-system-prompt)! So there are two ways to add them into an agent, which are in the agent or add from a  text file. Also, for long prompts, you can split different parts of it to differents txt files like tools, instructions, examples, and then add them into the agent code respectively. (for more, see next )


"""
1. Directly in code (simple, but messy)
"""
system_prompt = """
You are an expert AI assistant.

RULES:
1. Always answer clearly

WORKFLOW:
- Analyze problem

TOOLS:
- calculator

OUTPUT FORMAT:
{
  "analysis": "...",
  "final": "..."
}

... imagine 1000+ lines here ...
"""

# ----------------------------------------------------------------
"""
2. Store prompt in a separate file (recommended)
"""
# File: prompts/agent_system.txt
# Contents: Your 1000+ line prompt

def load_prompt(file_path):
    with open(file_path, "r", encoding="utf-8") as f:
        return f.read()

system_prompt = load_prompt("prompts/agent_system.txt")

# ----------------------------------------------------------------
"""
3. Use agent framework (LangChain example)
"""
from langchain.agents import initialize_agent

agent = initialize_agent(
    tools=tools,
    llm=llm,
    system_message=system_prompt
)

# ----------------------------------------------------------------
"""
4. Use multiple prompt files for large projects
"""
system_prompt = (
    open("prompts/role.txt").read() +
    open("prompts/rules.txt").read() +
    open("prompts/tools.txt").read()
)

# ----------------------------------------------------------------
"""
5. Combine role, tools, workflow, examples, safety rules, output format
   into one structured system prompt
"""
system_prompt = (
    open("prompts/role.txt").read() +
    "\n" +
    open("prompts/workflow.txt").read() +
    "\n" +
    open("prompts/examples.txt").read() +
    "\n" +
    open("prompts/safety.txt").read() +
    "\n" +
    open("prompts/output_format.txt").read()
)

# ----------------------------------------------------------------
"""
6. Store prompt in a variable for dynamic updates
"""
dynamic_prompt = "You are an AI assistant.\n"
dynamic_prompt += "Rules: 1. Be concise 2. Be accurate\n"
dynamic_prompt += "Workflow: analyze -> plan -> execute -> verify\n"
dynamic_prompt += "... more lines added programmatically ..."

# ----------------------------------------------------------------
"""
7. Use token-aware splitting for extremely long prompts
"""
def load_prompt_chunks(file_path, chunk_size=3000):
    """
    Load very long prompt and split into manageable chunks
    """
    with open(file_path, "r", encoding="utf-8") as f:
        text = f.read()
    return [text[i:i+chunk_size] for i in range(0, len(text), chunk_size)]

prompt_chunks = load_prompt_chunks("prompts/agent_system.txt")
# Then feed chunks sequentially to agent if needed








