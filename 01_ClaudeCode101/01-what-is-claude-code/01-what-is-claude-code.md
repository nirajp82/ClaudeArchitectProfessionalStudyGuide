# Lesson 1 — What is Claude Code?

> Course: [Claude Code 101](https://academy.claude.com/courses/claude-code-101) · Chapter 1: What is Claude Code?
> Completed: October 17, 2026
> ← [Course index](../README.md) · Next: [How Claude Code works](02-how-claude-code-works.md) →

---

### Definition

Claude Code is an **agentic coding tool**. It understands your codebase, edits files, runs commands, and integrates with your existing developer tools so you can get work done faster.

### Where it's available

- Terminal (CLI), which is what the lesson uses
- Visual Studio Code
- JetBrains IDEs
- Claude Desktop app
- Web

### Claude Code vs. Claude.ai

| | Claude.ai | Claude Code |
|---|---|---|
| Access to your files | No. You paste code in. | Yes, directly |
| Terminal access | No | Yes. Runs commands. |
| Codebase awareness | Only what you paste | Can explore the whole codebase |
| Workflow | Copy and paste back and forth | Does the work itself |
| Nature | Chat assistant | AI agent |

### What is an AI agent?

An **AI agent** is software that **interacts with its environment and performs actions to complete a defined goal**.

- The simplest form is a **large language model running in a loop** in real time.
- Agents have access to:
  - **Tools**
  - **External services**
  - **Other AI agents**

```text
        ┌──────────────────────────────┐
        │            Goal              │
        └──────────────┬───────────────┘
                       ▼
   ┌──────────►  LLM decides next step
   │                   │
   │                   ▼
   │       Act: read file / run command /
   │       edit code / search web
   │                   │
   │                   ▼
   └────────  Observe the result (output, errors)
                       │
                       ▼
               Goal reached → done
```

### What Claude Code can do (examples)

1. **Read and understand your codebase**: explain a feature, or trace a bug through the code.
2. **Run commands and use the output**: run build scripts and tests, install packages, then decide what to do next based on the results.
3. **Search the web**: for example, look up documentation for the latest API references.

### Three key concepts for using it well

#### 1. Context window = working memory
- Claude can hold a lot, but **not everything at once**.
- The agentic approach means it **searches strategically** for answers in your codebase instead of loading the whole codebase into context.

#### 2. It asks for permission
- By default, Claude Code **asks before running commands or changing your code**.
- **You stay in control**, and you choose how hands-on or hands-off to be.

#### 3. It can make mistakes
It might:
- misunderstand your intent
- introduce a new bug
- over-engineer a solution

→ Always review its changes. (This links to the study guide's rule: *verify, don't trust blindly*.)

### Recap

Claude Code is an agentic coding tool. It **reads your codebase, edits your files, runs commands, and connects to external tools** to help you ship faster. It's available in the terminal, VS Code, JetBrains, the Claude Desktop app, and on the web.

---

## My notes / practice

- [ ] Install Claude Code and run it in a test repo.
- [ ] Ask it to explain a feature of a small codebase.
- [ ] Ask it to run tests and fix one failure, reviewing each permission prompt.
- [ ] Note one mistake it made and how I caught it.

---

## FAQ

**Q1. What is Claude Code in one sentence?**
An agentic coding tool that reads your codebase, edits files, runs commands, and connects to external tools to help you get work done faster.

**Q2. How is Claude Code different from Claude.ai?**
Claude Code has direct access to your files, terminal, and codebase, so it can do the work itself. With Claude.ai you copy and paste code back and forth.

**Q3. What makes Claude Code an "agent"?**
It interacts with its environment and takes actions toward a defined goal. In its simplest form, that's an LLM running in a loop: decide, act, observe the result, repeat.

**Q4. What can an AI agent use to reach its goal?**
Tools, external services, and other AI agents.

**Q5. Where can I use Claude Code?**
The terminal, VS Code, JetBrains IDEs, the Claude Desktop app, and the web.

**Q6. What is the context window?**
Claude's working memory. It's large but limited, so Claude Code searches the codebase for what it needs instead of loading everything at once.

**Q7. Why doesn't Claude Code just load my whole codebase into context?**
Because the context window can't hold everything at once. Searching strategically and reading only the relevant files keeps the context focused. That's the agentic part of how it works.

**Q8. Will Claude Code change my files or run commands without asking?**
Not by default. It asks for permission before running commands or making changes. You decide how hands-on to be.

**Q9. Can Claude Code make mistakes?**
Yes. It can misunderstand your intent, introduce bugs, or over-engineer a solution, so review its changes and check them with tests.

**Q10. Give examples of tasks Claude Code can do.**
Explain a feature, trace a bug, run builds and tests, install packages, react to command output, and search the web for current API documentation.

**Q11. (Exam angle) Why does the permission model matter to an architect?**
It's a human-in-the-loop control. Consequential actions need approval, and that maps to the Governance, Safety & Risk domain and to the approval gate in the capstone project.

**Q12. (Exam angle) How does "it can make mistakes" affect how you design a workflow with Claude Code?**
Build in verification: code review, automated tests, clear acceptance criteria, and small bounded tasks. Never treat agent output as correct without checking it.
