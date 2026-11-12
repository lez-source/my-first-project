# Zero to First AI Agent: Weekend Plan (4 hours)

## 1. Where you're starting (from your answers)

| Question | Your answer | What it means for the plan |
|---|---|---|
| Coding level | Total beginner | We use Python, one small file, no frameworks. Every line gets explained. |
| Computer | Windows and Mac, equally | Install steps for both. Everything is saved to GitHub, so you can switch machines. |
| Time | About 4 hours | Four 1-hour blocks. The agent is deliberately small so it can be finished. |
| Task | Ideas for freelancers (Amazon media buyer, Canva templates, etc.) | The agent is a **Freelance Starter Scout** (see section 3). |

**Cost note:** a Claude Pro subscription does not include API access. The agent calls Claude through the API, which is billed separately at console.anthropic.com. Expect a few dollars of credit to be plenty: one agent run costs cents. Don't share your API key, and never commit it to GitHub.

## 2. Concepts, in order (each one is needed by the next)

1. **What an agent is.** An LLM that can *act*: it gets a goal, picks a tool, sees the result, and repeats until done. A chatbot only talks; an agent does things.
2. **Python basics you actually need:** variables, strings, lists, dictionaries, functions, `if`, `for`/`while`, reading and writing a file. About 8 ideas total.
3. **Terminal basics:** `cd`, `ls`/`dir`, running `python file.py`.
4. **APIs and keys:** your program sends a message to Claude over the internet and gets text back. The key is your password; it lives in an environment variable, not in code.
5. **Messages:** a conversation is a list of messages (`user`, `assistant`).
6. **Tools:** you describe a function to Claude (name, what it does, inputs). Claude replies "please run this tool with these inputs". *Your* code runs it and sends back the result.
7. **The agent loop:** keep calling Claude, run any tools it asks for, feed the results back, stop when it answers without asking for a tool.
8. **Testing:** prove it works with checks that don't depend on how the model words things.

## 3. The first project: Freelance Starter Scout

**You type:** a freelance path, for example `Canva template seller` or `Amazon media buyer`.

**The agent:**
1. Asks Claude to build a starter plan: skills to learn, first 3 steps, tools, how to get a first client or sale.
2. Uses its **tools** to ground the plan in numbers instead of guesses:
   - `estimate_income(hourly_rate, hours_per_week)` returns monthly income. It is plain Python maths, so it's exactly right every time.
   - `save_plan(filename, text)` writes the final plan to a `plans/` folder as a Markdown file.
3. Stops when the plan is saved and tells you where it is.

It is a real agent because it decides for itself which tools to call, and in what order, to reach the goal. It's small enough to understand completely.

**Honesty rule built into the agent:** it must label income figures as *assumptions you set*, not promises, and must not invent specific earnings claims.

## 4. Tools to install

| Tool | Windows | Mac |
|---|---|---|
| Python 3.12+ | python.org installer, **tick "Add Python to PATH"** | `brew install python` or python.org installer |
| Git | git-scm.com installer | Comes with Xcode tools: run `git --version` and accept the prompt |
| VS Code (editor) | code.visualstudio.com | code.visualstudio.com |
| Anthropic SDK | `pip install anthropic` | `pip3 install anthropic` |
| API key | console.anthropic.com, create a key | same |

Set the key as an environment variable:
- Windows (PowerShell): `setx ANTHROPIC_API_KEY "your-key"` then reopen the terminal
- Mac: add `export ANTHROPIC_API_KEY="your-key"` to `~/.zshrc`, then `source ~/.zshrc`

Check everything: `python --version`, `git --version`, `pip show anthropic`.

## 5. Schedule and milestones

### Saturday, Block 1 (1 hour): Setup and first contact
- Install the tools above, clone this repo, open it in VS Code.
- Learn: terminal basics, running a Python file.
- **Milestone:** a 10-line script sends "Say hello" to Claude and prints the reply.

### Saturday, Block 2 (1 hour): Python and messages
- Learn: variables, functions, dictionaries, lists, with small exercises.
- Change the script to take your input and answer as a freelance coach.
- **Milestone:** `python coach.py "Canva template seller"` prints a starter plan. First commit pushed to GitHub.

### Sunday, Block 3 (1 hour): Tools
- Write `estimate_income` and `save_plan` as normal Python functions and test each by hand.
- Describe them to Claude so it can request them.
- **Milestone:** Claude asks to use a tool, your code runs it, you see the result printed.

### Sunday, Block 4 (1 hour): The loop and the test
- Wrap it in the agent loop. Add the honesty rule to the instructions.
- Run the test in section 6.
- **Milestone:** all checks pass and `plans/` contains a saved plan.

**If you fall behind:** drop Block 2's exercises, never the Block 4 test. A smaller agent that passes beats a bigger one that doesn't.

## 6. The test that proves it works

A good test checks **behaviour**, not wording, because the model's text changes every run. Run `python test_agent.py` with the input `Canva template seller`. All five must pass:

1. **Runs to completion:** the loop ends without errors in under 10 steps.
2. **Used its tools:** the log shows `estimate_income` was called and `save_plan` was called.
3. **File exists:** a new `.md` file appears in `plans/` and is not empty.
4. **Numbers are right:** the income figure in the file matches `estimate_income` called directly with the same inputs.
5. **Honest:** the file contains the word "assumption" and no phrases like "guaranteed" or "you will earn".

Bonus: run it with `Amazon media buyer` and confirm it passes again on a different input.

## 7. After the weekend (ideas, in order of difficulty)
1. Add a web search tool so plans use current information.
2. Add a `find_clients` tool that drafts outreach messages.
3. Turn the Canva idea into a second agent that outlines a template pack.
4. Schedule it to run weekly and save a "freelance opportunities" digest.

## 8. Rules for learning faster
- Type the code yourself rather than pasting it; it sticks better.
- When something breaks, read the **last line** of the error first. Then ask me.
- Commit after every milestone (`git add .`, `git commit -m "what I did"`, `git push`).
- Ask "why" often. Understanding beats speed.
