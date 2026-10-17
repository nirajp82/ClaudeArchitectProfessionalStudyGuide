# Lesson 2 — How Claude Code works

> Course: [Claude Code 101](https://academy.claude.com/courses/claude-code-101) · Chapter 1: What is Claude Code?
> Completed: October 17, 2026
> ← Previous: [What is Claude Code?](01-what-is-claude-code.md) · [Course index](README.md) · Next: [Installing Claude Code](03-installing-claude-code.md) →

---

### The big picture

Claude Code is built from four parts working together inside your terminal:

1. **The agentic loop**: how it works through a task step by step.
2. **The context window**: what Claude can see and remember during the task.
3. **Tools**: how Claude actually does things, instead of only writing text.
4. **Permissions**: how you control which actions it's allowed to take.

Because of these four parts, Claude Code can read your codebase, take action, and check its own work. A chat window can't do any of that.

### 1. The agentic loop

The agentic loop is the cycle Claude Code repeats until your task is done.

1. **You enter a prompt.** For example, "fix the failing login test."
2. **Gather context.** Claude works out what it needs to know. The model replies with either text or a **tool call**, which is a request for Claude Code to do something, such as open a file or search the code. Claude Code runs the tool and gives the result back to the model.
3. **Take action.** Claude makes a change, such as editing a file or running a command.
4. **Verify the results.** Claude checks whether the change actually does what your prompt asked. For example, it runs the test again.
5. **Finish or loop again.**
   - If the results are good, Claude stops and waits for your next prompt.
   - If they aren't, Claude goes back to step 2 and tries again. It keeps going until the result is complete and can be checked.

```text
          Your prompt
               │
               ▼
     ┌──► Gather context ──┐
     │                     ▼
     │               Take action
     │                     │
     │                     ▼
     └─── not done ── Verify results
                           │
                         done
                           ▼
                Wait for next prompt

   At any point, you can: add context · interrupt · steer
```

**You can step in at any time.** While the loop runs, you can:
- **Add context**: give it information it's missing, such as "the config file is in `/settings`."
- **Interrupt**: stop it if it's going the wrong way.
- **Steer**: change its direction, such as "don't touch the database code, just fix the test."

The key difference from a chatbot is step 4. A chatbot gives one answer and stops. Claude Code checks whether its work actually succeeded and keeps going if it didn't.

### 2. The context window

The **context window** is everything Claude can see and look back on during a session. That includes your conversation, the contents of files it has read, and the output of commands it has run.

The window has a size limit. When a long session fills it up, Claude Code **compacts** the conversation:
- It decides what's no longer needed and **removes** it.
- It **summarizes** what's still useful into a shorter form.

This brings the context back down to a usable size so the session can continue. It happens automatically.

The trade-off: a summary keeps the main points but loses detail. After compacting, Claude may no longer remember an exact earlier message or file it read.

### 3. Tools

**Tools are what make Claude Code an agent.** Most AI assistants only take text in and give text out. There's nothing in between: they can describe what to do, but they can't do it.

A **tool** is an ability Claude can use to act in the real world. Examples:
- **Read file**: open and read a file in your project.
- **Search the web**: look up current information.
- Others, such as editing files or running shell commands.

Claude decides **for itself** when a tool is needed. It understands what your request means (this is called *semantic understanding*), picks the right tool, runs it, and uses the result to decide what to do next. You don't have to tell it "now read this file." It figures out that it needs to.

### 4. Permissions

**Permission modes** control what Claude Code can do without asking you first. You can switch between modes with **Shift+Tab**.

| Mode | File edits | Shell commands | When to use it |
|---|---|---|---|
| **Manual** | Asks first | Asks first | You want to approve every step. |
| **Auto-accept** | No prompt | Asks first | You trust it to edit code, but want to check commands before they run. |
| **Plan mode** | Not allowed | Read-only only | You want a plan of action before any work starts. |
| **Auto mode** | No prompt | No prompt, but checked | You want it to work without interruptions, with a safety check in the background. |

More about each mode:
- **Manual**: Claude asks for your approval before every file edit or shell command.
- **Auto-accept**: edits happen without asking, because they're easy to review afterward. Commands still need approval, because they can have effects outside your files (installing packages, deleting things, calling services).
- **Plan mode**: Claude only uses read-only tools, so it can look around but can't change anything. It uses what it learns to write a plan for you to review before starting.
- **Auto mode**: Claude doesn't stop to ask. Instead, a **classifier** (a separate check) reviews each action in the background. It's designed to block actions that are:
  - **irreversible**: can't be undone
  - **destructive**: could delete or break things
  - **aimed outside your environment**: affect systems beyond your project

  When an action is blocked, Claude usually finds a safer way to do it, or asks you for permission.

Which mode a new session starts in depends on your Claude Code version and settings. All of this can be configured in your **settings file**.

**Be careful when skipping permissions.** If Claude can run any command without asking, a mistake can happen before you get a chance to catch it. The more freedom you give it, the less chance you have to stop a bad action.

### Recap

Claude Code combines four agentic concepts inside your terminal:

1. **An agentic loop**: gather context, take action, verify, and repeat until done.
2. **A managed context window**: it compacts automatically when it gets full.
3. **Tools**: they let it actually do things instead of only writing text.
4. **Configurable permissions**: you decide how much it can do without asking.

Together, these let Claude Code read your codebase, take action, and verify its own work. That's what makes it fundamentally different from a chat window.

---

## My notes / practice

- [ ] Give Claude Code a small task and watch the loop: note when it gathers context, acts, and verifies.
- [ ] Interrupt a task partway through and steer it in a different direction.
- [ ] Press Shift+Tab to cycle through the permission modes and note which one the session starts in.
- [ ] Use plan mode to get a plan for a change before letting it edit anything.
- [ ] Find where permission settings live in my settings file.

---

## FAQ

**Q1. What is the agentic loop?**
The cycle Claude Code repeats to finish a task:
1. You give a prompt.
2. It gathers context.
3. It takes action.
4. It verifies the results.

If the results are good, it stops and waits for your next prompt. If not, it goes back to step 2 and tries again.

**Q2. What happens during the "gather context" step?**
Claude works out what it needs to know. The model returns either text or a **tool call**, a request for Claude Code to do something like read a file or search the code. Claude Code runs the tool and passes the result back to the model.

**Q3. Why does the "verify" step matter?**
It's what separates Claude Code from a chatbot. A chatbot gives one answer and stops, whether or not the answer works. Claude Code checks whether its change actually achieved the goal (for example, by re-running a test) and keeps trying if it didn't.

**Q4. Can I change what Claude is doing while the loop is running?**
Yes. At any point you can:
- **add context**: tell it something it doesn't know
- **interrupt**: stop it
- **steer**: change its direction

**Q5. What happens when the context window fills up?**
Claude Code **compacts** the conversation automatically. It removes what's no longer needed and summarizes the rest, which brings the context back to a usable size so the session can continue. Summaries lose detail, so after compacting, Claude may not remember exact earlier content.

**Q6. Why are tools called "the backbone" of agents?**
Without tools, an AI can only take text in and give text out. It can describe a fix, but it can't apply it. Tools such as reading files, editing files, running commands, or searching the web let Claude actually do the work.

**Q7. How does Claude decide when to use a tool?**
It understands what your request means (semantic understanding) and decides for itself which tool would help, such as reading a file before editing it. It then uses the tool's output to decide what to do next. You don't have to tell it which tool to use.

**Q8. What are the permission modes?**
- **Manual**: asks before every file edit and shell command.
- **Auto-accept**: edits files without asking, but still asks before running commands.
- **Plan mode**: read-only. It looks around and writes a plan before making any changes.
- **Auto mode**: no prompts. A background classifier blocks risky actions.

You switch between modes with **Shift+Tab**, and you can configure them in your settings file.

**Q9. Why does auto-accept still ask before running commands?**
File edits are easy to see and undo. Commands can have effects beyond your files, such as installing packages, deleting data, or calling outside services, and some of those can't be undone. So commands still need your approval.

**Q10. In auto mode, what does the classifier block?**
Actions that are **irreversible** (can't be undone), **destructive** (could delete or break things), or **aimed outside your environment** (affect systems beyond your project). When an action is blocked, Claude usually finds a safer approach or asks you for permission.

**Q11. (Exam angle) How would you choose a permission mode for a team?**
Match how much freedom Claude gets to how risky the work is:
- **Plan mode** for unfamiliar or high-stakes code: review the approach before anything changes.
- **Manual** or **auto-accept** for normal work, so a person still approves commands.
- **Auto mode** only where its background checks are enough for that environment.

Set this in the settings file so the whole team gets the same behavior instead of each person deciding. This maps to the **Governance, Safety & Risk** domain.

**Q12. (Exam angle) Why is skipping permissions risky, and what reduces the risk?**
If Claude can run any command without asking, a mistake can take effect before anyone sees it. To reduce the risk:
- Keep a person approving actions that can't be undone.
- Use plan mode to agree on the approach first.
- Run Claude in an isolated environment, so a bad command can't reach real systems.
- Rely on the verify step and tests to catch errors after changes.
