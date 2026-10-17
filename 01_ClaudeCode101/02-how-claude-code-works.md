# Lesson 2 — How Claude Code works

**Course:** [Claude Code 101](https://academy.claude.com/courses/claude-code-101) &nbsp;·&nbsp; **Chapter 1:** What is Claude Code? &nbsp;·&nbsp; **Completed:** October 17, 2026

| Previous | Course | Next |
|:---|:---:|---:|
| [← What is Claude Code?](01-what-is-claude-code.md) | [📚 Course index](README.md) | [Installing Claude Code →](03-installing-claude-code.md) |

---

**On this page**

| # | Section |
|:---:|:---|
| 1 | [In one sentence](#in-one-sentence) |
| 2 | [The four parts](#the-four-parts) |
| 3 | [1. The loop: look, do, check, repeat](#1-the-loop-look-do-check-repeat) |
| 4 | [2. The context window: what Claude can remember right now](#2-the-context-window-what-claude-can-remember-right-now) |
| 5 | [3. Tools: how Claude actually does things](#3-tools-how-claude-actually-does-things) |
| 6 | [4. Permissions: what Claude can do without asking](#4-permissions-what-claude-can-do-without-asking) |
| 7 | [5. Behind the scenes: your computer vs. Anthropic's servers](#5-behind-the-scenes-your-computer-vs-anthropics-servers) |
| 8 | [Recap](#recap) |
| 9 | [My notes / practice](#my-notes--practice) |
| 10 | [FAQ](#faq) |

---

### In one sentence

Claude Code works like a helper who doesn't give up after one try. It **looks** at your code, **makes a change**, **checks** if the change worked, and **tries again** if it didn't.

### The four parts

| Part | What it means in plain words |
|---|---|
| **1. The loop** | It repeats *look → do → check* until the job is done. |
| **2. The context window** | What Claude can remember right now. |
| **3. Tools** | The things Claude can actually do, like open a file or run a command. |
| **4. Permissions** | What Claude is allowed to do without asking you first. |

Section 5 then shows how they fit together: what happens on your computer and what happens on Anthropic's servers.

We'll use one example through the whole lesson:

> **You:** "The login test is failing. Fix it."

---

### 1. The loop: look, do, check, repeat

Think of a mechanic fixing a strange noise in a car. They listen to the engine, replace a part, then start the car to hear if the noise is gone. If it's still there, they try something else. They keep going until the noise stops.

Claude Code works the same way. The course calls this the **agentic loop**.

**Step 1. You ask.**
"The login test is failing. Fix it."

**Step 2. Claude looks around.** (The course calls this *gathering context*.)
Claude doesn't know your code yet, so it explores first. It opens the test file, runs the test to see the error, and finds the login code.

**Step 3. Claude makes a change.** (The course calls this *taking action*.)
It edits the login code to fix the problem.

**Step 4. Claude checks its work.** (The course calls this *verifying results*.)
It runs the test again.

**Step 5. Done, or go round again.**
- The test passes → Claude stops and waits for your next request.
- The test still fails → Claude goes back to Step 2, reads the new error, and tries again.

Here's what that looks like in a real session:

```text
You:    The login test is failing. Fix it.

Claude: opens tests/login.test.js           ← look
        runs the test, reads the error       ← look
        opens src/login.js                   ← look
        edits src/login.js                   ← do
        runs the test again → still fails    ← check: not done yet, go round again
        reads the new error                  ← look
        edits src/login.js again             ← do
        runs the test again → passes ✅      ← check: done

Claude: Fixed. The password check was comparing the wrong field.
```

<img width="3840" height="2160" alt="image" src="https://github.com/user-attachments/assets/183c87f2-2032-4b41-8a72-6b43d8f70a3f" />

#### Who does the work: the brain and the hands

"Claude" is really two things working together:
- **The model** is the **brain**. It runs on Anthropic's servers. It thinks and decides, but it **can't touch your computer**.
- **Claude Code** is the **hands**. It's the program on your computer. It opens files, edits them, and runs commands.

When the brain wants to see a file, it asks the hands: *"please open `src/login.js`."* That request is called a **tool call**. The hands open the file and send the contents back.

Every reply from the model is one of two things:
- a **tool call**: "do this for me," so the loop keeps going
- **plain text**: "here's my answer," so the loop ends

👉 [Section 5](#5-behind-the-scenes-your-computer-vs-anthropics-servers) walks through this message by message.

#### You can jump in at any time

You don't have to wait for Claude to finish. While it's working, you can:

| You can... | Example |
|---|---|
| **Add information** | "The login settings are in `config/auth.json`." |
| **Stop it** | Claude is changing files you didn't expect. You stop it. |
| **Change its direction** | "Don't touch the database code. Only fix the test." |

#### Why this matters

A normal chatbot gives you one answer and hopes it works. It never finds out. Claude Code **checks its own work** and keeps going until it actually works. That's the big difference.

---

### 2. The context window: what Claude can remember right now

Think of a **whiteboard**. Everything from your session gets written on it:
- your messages
- Claude's replies
- the files Claude opened
- the output of commands it ran

Claude can only use what's on the whiteboard. The whiteboard is big, but it **has a fixed size**.

#### What happens when it fills up

When the whiteboard is full, Claude Code **compacts** it. This means it cleans it up so the session can keep going:
- It **erases** things that aren't needed anymore.
- It **replaces long parts with short summaries**.

For example, 500 lines of test output from an hour ago might become one line: *"Ran the tests. 2 failed, both in login."*

This happens **automatically**. You don't have to do anything.

**The downside:** a summary loses detail. If Claude needs something exact from much earlier, like a specific error message, it may not have it anymore. Just tell it again or ask it to look again.

---

### 3. Tools: how Claude actually does things

Imagine your car breaks down and you **phone a friend** who knows cars. They can tell you what to try, but they can't touch the car. You do all the work.

Now imagine that friend is **standing next to the car with a wrench**. They can do the work themselves.

- Most AI chat apps are the friend on the phone. Text goes in, text comes out. That's it.
- **Tools** turn Claude into the friend with the wrench.

A **tool** is one specific thing Claude is able to do:

| Tool | Example of what Claude does with it |
|---|---|
| Read a file | Opens `src/login.js` to see how login works. |
| Edit a file | Changes one line in `src/login.js` to fix the bug. |
| Run a command | Runs `npm test` to check if the tests pass. |
| Search the web | Looks up the current docs for a library you use. |

**Claude picks the right tool by itself.** It understands what you *mean* (the course calls this *semantic understanding*) and decides what it needs to do.

For example, you ask: *"Why does the login page crash?"*
You don't say "read the file" or "run the app." Claude works out on its own that it should open the login code and look at the error.

---

### 4. Permissions: what Claude can do without asking

Think of a **new assistant** on their first day. You decide which keys to give them. Maybe they can edit documents but have to ask before using the company credit card.

Permissions work the same way. They decide what Claude can do on its own and what it has to ask you about first.

By default, Claude **asks you before it edits a file or runs a command**. You see the exact action and choose to allow it or say no.

<!-- IMAGE: Claude Code asking for permission before running a bash command → images/02-permission-prompt.png -->

#### The four modes

You can switch between modes by pressing **Shift+Tab**.

| Mode | Edits files without asking? | Runs commands without asking? | Good for |
|---|---|---|---|
| **Manual** | ❌ Asks | ❌ Asks | Learning, or important code where you want to see every step |
| **Auto-accept** | ✅ Yes | ❌ Asks | Everyday work: let it edit, but check commands |
| **Plan mode** | ❌ Can't edit at all | Only looks, changes nothing | Big or unfamiliar changes: see the plan first |
| **Auto mode** | ✅ Yes | ✅ Yes, but a safety check watches | Long tasks where you don't want to keep clicking "allow" |

**Manual: Claude asks before every edit and every command.**
You approve each step one by one. It's slower, but you see everything.

**Auto-accept: edits happen on their own, but commands still need your OK.**
Why the difference? An edit is easy to see and undo afterward. A command can do things that are hard to undo, like deleting a folder or installing software. So commands still ask.

**Plan mode: Claude only looks. It doesn't change anything.**
It reads your code and writes a step-by-step plan. You read the plan and decide whether to go ahead.
*Example:* "Plan how to add a dark mode." Claude reads your files and replies with a list: which files to change, and what to change in each.

**Auto mode: Claude doesn't stop to ask, but a separate safety checker watches every action.**
The checker blocks actions that are dangerous:
- **can't be undone**, for example deleting a database
- **destroys things**, for example wiping a folder
- **reaches outside your project**, for example sending files to another website or changing a live server

If an action is blocked, Claude usually finds a safer way to do it, or asks you.

#### Good to know

- Which mode you **start** in depends on your Claude Code version and your settings.
- You can set all of this in your **settings file**.

#### ⚠️ Be careful about turning off the questions

When Claude asks first, you get a chance to say **"no, wait"** before a mistake happens. When it doesn't ask, the mistake happens first and you find out later.

*Example:* Claude misunderstands you and runs a command that deletes files you haven't saved to Git yet. In Manual mode, you would have seen the command and said no. With no questions asked, the files are already gone.

---

### 5. Behind the scenes: your computer vs. Anthropic's servers

This section puts the four parts together. It answers the question: **"When I type a request, what happens on my computer, and what happens on Anthropic's servers?"**

#### 🧠 Remember this

> **Brain on the server. Hands on your computer.**
> The model **asks**. Claude Code **does**. You **approve**.

#### Two programs, two computers

| | **Claude Code** (on your computer) | **The model** (on Anthropic's servers) |
|---|---|---|
| What it is | A program you installed | The AI brain |
| Can see your files? | ✅ Yes | ❌ No. It only sees what Claude Code sends it. |
| Can run commands? | ✅ Yes | ❌ No |
| Remembers the conversation? | ✅ Yes. It keeps the full history. | ❌ No. It forgets everything after each reply. |
| Its job | **Hands**: read, edit, run, and ask your permission | **Brain**: think and decide the next step |

They never share a screen or a disk. They only talk by **sending messages over the internet**.

#### Example: "The login doesn't work"

Each round below is **one message from Claude Code to the server, and one reply back**.

| Round | 💻 On your computer (Claude Code) | ☁️ On the server (the model) |
|:---:|---|---|
| **1** | You type *"The login doesn't work."* Claude Code sends your request, plus a list of the tools it has ("I can read files, search, edit, run commands…") and basic facts like which folder you're in. | Thinks: *"I don't know this code yet. Find the login code."* Replies with a tool call: 🔧 **Search for "login"** |
| **2** | Searches **your disk**. Finds `src/login.js` and `tests/login.test.js`. Sends back **everything so far + the search result**. | Thinks: *"Look at the login code."* Replies: 🔧 **Read `src/login.js`** |
| **3** | Opens the file **from your disk**. Sends back **everything so far + the file's contents**. | Reads the code. Spots the bug: line 12 compares the password to `user.email`. Replies: 🔧 **Edit line 12 to use `user.password`** |
| **4** | Asks **you**: *"Allow edit to src/login.js?"* You click Yes. Changes the file **on your disk**. Sends back **everything so far + "edit done."** | Thinks: *"Now check it works."* Replies: 🔧 **Run `npm test`** |
| **5** | Asks **you**: *"Allow command `npm test`?"* You click Yes. Runs the tests **on your computer**. Sends back **everything so far + "5 tests passed."** | Thinks: *"It works."* Replies with **plain text, no tool call**: 💬 *"Fixed. Line 12 was comparing the email instead of the password."* |
| **End** | The reply has **no tool call**, so Claude Code knows the job is done. It shows you the message and waits. | Nothing. It has already forgotten all of this. |

The same thing as a picture:

```text
  YOUR COMPUTER                                    ANTHROPIC'S SERVERS
  Claude Code = the hands                          The model = the brain
  -----------------------                          ---------------------

  You: "The login doesn't work."
     |
     |-- (1) your request + tool list -------------->  "Find the login code."
     |<------------------------------------------------ TOOL CALL: search "login"
  searches your disk, finds src/login.js
     |
     |-- (2) everything so far + search result ----->  "Read that file."
     |<------------------------------------------------ TOOL CALL: read src/login.js
  opens the file from your disk
     |
     |-- (3) everything so far + file contents ----->  "Line 12 is wrong."
     |<------------------------------------------------ TOOL CALL: edit line 12
  asks YOU "Allow edit?" -> Yes
  changes the file on your disk
     |
     |-- (4) everything so far + "edit done" ------->  "Now test it."
     |<------------------------------------------------ TOOL CALL: run npm test
  asks YOU "Allow command?" -> Yes
  runs the tests on your computer
     |
     |-- (5) everything so far + "5 passed" -------->  "It works."
     |<------------------------------------------------ TEXT: "Fixed. Line 12..."
  no tool call -> loop ends
  shows you the answer
```

#### What one message actually contains

Here is a simplified view of **message 3**. Notice that it repeats everything from rounds 1 and 2:

```text
Message 3, sent from your computer to the server
------------------------------------------------
Instructions:  You are Claude Code. Tools you can use: Search, Read, Edit, Run...
You:           The login doesn't work.
Model:         [tool call] Search for "login"
Claude Code:   [result]    src/login.js, tests/login.test.js
Model:         [tool call] Read src/login.js
Claude Code:   [result]    (all 40 lines of login.js)
```

By message 5, it also contains the edit and the test output. This growing message **is the context window** from section 2. When it gets too big, Claude Code **compacts** it.

#### Four facts that clear up the confusion

**1. The model forgets everything after each reply.**
It has no memory between messages. That's why Claude Code **sends the whole conversation every time**. Claude Code holds the memory; the model just reads it fresh each round.

**2. The model only sees what Claude Code sends it.**
It doesn't have your hard drive. It saw `login.js` only because it asked to read that file. Your other files never left your computer.
⚠️ But a file that **was** read **did** go to the server. Don't let Claude read files with passwords or secret keys unless you mean to.

**3. All the real work happens on your computer.**
Searching, reading, editing, and running tests all happen on your machine, using your files, your tools, and your processor. The model only sends instructions ("run `npm test`") and gets the output back as text. So if your tests need a database running on your laptop, that works fine. Your laptop is the one running them.

**4. Permissions are checked on your computer, before anything runs.**
The model can **ask** for anything, even something dangerous. Claude Code decides whether to do it, and checks your permission mode first. The model has no other way to act, so it can't get around your permissions.

#### Common mix-ups

| ❌ Wrong idea | ✅ What really happens |
|---|---|
| "The model reads my whole codebase." | It only sees the files it asked to read. |
| "My tests run in the cloud." | They run on your computer. The model only sees the output. |
| "The model remembers what we did." | It forgets after every reply. Claude Code resends the history each time. |
| "The model could delete my files directly." | It can't touch your files. It can only ask Claude Code, and Claude Code checks your permissions first. |
| "Permissions are controlled by Anthropic's servers." | They're checked by Claude Code, on your computer. |

> **Note:** If you use Claude Code **on the web** or in a **cloud environment** (lesson 3), "your computer" is a remote machine that runs your code instead of your laptop. The split is the same: the brain on Anthropic's model servers, and the hands on the machine where your code lives.

#### Test yourself

<details>
<summary>1. You ask Claude to fix a bug. Where does the file actually get changed?</summary>

On your computer. The model only sends the instruction "edit this line." Claude Code makes the change on your disk, after checking your permission.
</details>

<details>
<summary>2. How does Claude Code know the job is finished?</summary>

The model replies with plain text instead of a tool call. No tool call means there's nothing left to do, so the loop ends.
</details>

<details>
<summary>3. Why does each message get bigger as the task goes on?</summary>

The model forgets everything after each reply, so Claude Code resends the whole conversation every time, plus the newest result. That growing message is the context window.
</details>

<details>
<summary>4. Does the model see a file Claude never opened?</summary>

No. Only what Claude Code sends gets to the server. Files that were never read stay on your computer.
</details>

---

### Recap

- **The loop:** Claude looks, makes a change, checks if it worked, and repeats until it does. You can add information, stop it, or redirect it at any time.
- **The context window:** what Claude can remember right now. When it fills up, Claude Code automatically summarizes old parts to make room. Some detail gets lost.
- **Tools:** what let Claude actually *do* things (read files, edit files, run commands, search the web) instead of only talking. Claude picks the right tool itself.
- **Permissions:** you decide what Claude can do without asking. Switch modes with Shift+Tab: Manual, Auto-accept, Plan mode, or Auto mode.
- **Behind the scenes:** the brain (the model) is on Anthropic's servers. The hands (Claude Code) are on your computer. The model asks, Claude Code does, you approve. The model forgets after every reply, so Claude Code resends the whole conversation each time. The loop ends when the model replies with text instead of a tool call.

Together, these are why Claude Code can do the work and check it, and not just chat about it.

---

## My notes / practice

- [ ] Give Claude Code a small task and watch the loop. Spot when it looks, when it changes something, and when it checks.
- [ ] Stop it partway through a task and give it a new direction.
- [ ] Press Shift+Tab to cycle through the modes. Note which mode a new session starts in.
- [ ] Use Plan mode to get a plan for a change before letting Claude edit anything.
- [ ] Find the permission settings in my settings file.
- [ ] Ask Claude to fix something small. For each step, say out loud whether it happened on my computer or on the server.

---

## FAQ

**Q1. How does Claude Code work, in simple terms?**
It repeats a loop: look at the code, make a change, check if it worked. If it didn't work, it goes round again. If it did, it stops and waits for you.

**Q2. What does "gather context" mean?**
It means looking around before acting. Claude opens files, runs commands, and reads errors so it understands the problem before changing anything.

**Q3. What is a tool call?**
A request from the model to Claude Code, such as "open this file" or "run this command." The model can't touch your computer itself, so it asks Claude Code to do it. Claude Code does it and sends back the result.

**Q4. Why is checking its own work so important?**
A chatbot gives one answer and never finds out if it worked. Claude Code runs the test (or checks some other way) and keeps trying until it actually works.

**Q5. Can I change what Claude is doing while it works?**
Yes. You can add information ("the settings are in `config/auth.json`"), stop it, or change its direction ("only fix the test").

**Q6. What is the context window?**
Everything Claude can remember right now: your messages, its replies, files it opened, and command output. Think of it as a whiteboard with a fixed size.

**Q7. What happens when the context window is full?**
Claude Code **compacts** it automatically. It erases what isn't needed and summarizes the rest so the session can keep going. Some detail is lost, so if Claude needs something exact from much earlier, tell it again.

**Q8. Why are tools so important?**
Without tools, an AI can only talk. It can tell you how to fix something, but it can't do it. Tools let Claude read files, edit files, run commands, and search the web, so it does the work itself.

**Q9. Do I have to tell Claude which tool to use?**
No. It understands what you mean and picks the tool itself. If you ask "why does the login page crash?", it decides on its own to open the login code and look at the error.

**Q10. What are the four permission modes?**
- **Manual:** asks before every edit and every command.
- **Auto-accept:** edits without asking, but asks before commands.
- **Plan mode:** only looks and writes a plan. Changes nothing.
- **Auto mode:** doesn't ask, but a safety checker blocks dangerous actions.

Switch between them with **Shift+Tab**.

**Q11. Why does auto-accept still ask before running commands?**
An edit is easy to see and undo. A command can do things that are hard to undo, like deleting files or installing software. So commands still need your OK.

**Q12. In auto mode, what does the safety checker block?**
Actions that can't be undone (like deleting a database), that destroy things (like wiping a folder), or that reach outside your project (like sending files to another website). If something is blocked, Claude tries a safer way or asks you.

**Q13. What runs on my computer, and what runs on Anthropic's servers?**
- **Your computer:** Claude Code, the hands. It searches, reads, and edits files, runs commands, asks your permission, and keeps the conversation history.
- **Anthropic's servers:** the model, the brain. It reads the messages Claude Code sends and decides the next step.

**Q14. Does the model see my whole codebase?**
No. It only sees what Claude Code sends: your messages, plus the results of the tools it asked for, such as the files it read. Files that were never read stay on your computer.

**Q15. The model forgets everything after each reply. So how does it follow a long task?**
Claude Code sends the **whole conversation** with every message: your request, every tool call, every file read, every result. The model reads it all fresh each time. That growing message is the context window.

**Q16. Isn't sending the whole conversation every time slow and wasteful?**
Less than it sounds. Anthropic's servers can reuse the parts of a message they've already seen (this is called *prompt caching*), so repeating the history is faster and cheaper than processing it from scratch.

**Q17. When Claude "runs the tests," where do they run?**
On your computer. Claude Code runs the command using your files and your tools. The model only sends the instruction and reads the output that comes back.

**Q18. How does Claude Code know the loop is finished?**
The model replies with plain text instead of a tool call. No tool call means there's nothing left to do.

**Q19. Could the model delete my files directly?**
No. It can't touch your computer. It can only *ask* Claude Code, and Claude Code checks your permission mode before doing anything.

**Q20. (Exam angle) How should a team choose a permission mode?**
Give Claude less freedom when mistakes would be costly:
- **Plan mode** for big or risky changes, so a person approves the plan first.
- **Manual** or **auto-accept** for everyday work, so a person still approves commands.
- **Auto mode** only where its safety checks are good enough for that project.

Put the choice in the settings file so the whole team works the same way, instead of each person deciding. This fits the **Governance, Safety & Risk** exam domain.

**Q21. (Exam angle) Why is turning off permission questions risky, and how do you reduce the risk?**
Without the questions, a mistake happens before anyone can stop it. To reduce the risk:
- Keep a person approving anything that can't be undone.
- Use Plan mode to agree on the approach first.
- Run Claude in a separate test environment, so a bad command can't harm real systems.
- Use tests to catch mistakes after changes are made.

**Q22. (Exam angle) A security team asks, "What data leaves our machines when developers use Claude Code?" How do you answer?**
- **What leaves:** the messages Claude Code sends to the model. That means the developer's requests, plus the results of any tools Claude used: the contents of files it read, command output, search results.
- **What stays:** everything Claude never read or ran. The code runs, the files change, and commands execute on the developer's machine.
- **How to control it:** limit what Claude can read and run with permission settings, keep secrets out of files Claude is likely to open, and set these rules centrally for the team.

This fits the **Governance, Safety & Risk** exam domain.

---

| Previous | Course | Next |
|:---|:---:|---:|
| [← What is Claude Code?](01-what-is-claude-code.md) | [📚 Course index](README.md) | [Installing Claude Code →](03-installing-claude-code.md) |
