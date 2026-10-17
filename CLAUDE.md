# Study guide rules

This repo holds my study notes for the Claude Architect Professional exam. These rules apply to every lesson note, every time.

## Writing lesson notes

The transcript and course text I paste are **reference only**. They tell you what the lesson covers. Don't just tidy them up. Put in extra effort so a beginner understands each idea on the first read.

1. **Use plain English. Write for a beginner, as if explaining to a friend.**
   - Short sentences. One idea per sentence. Everyday words.
   - Lead with the plain idea, then give the course's term in brackets: "Claude looks around first (the course calls this *gathering context*)." Don't lead with jargon.
   - Define every technical term the first time it appears, such as "a tool call is a request for Claude Code to do something."
   - Use an everyday comparison for each big idea, such as a mechanic for the loop or a whiteboard for the context window.
   - Pick one running example for the lesson and use it all the way through.
   - Open with an "In one sentence" summary.
   - No marketing words or filler.
   - Model: `01_ClaudeCode101/02-how-claude-code-works.md`.

2. **Make it clear, not just shorter.**
   - Explain *why*, not only *what*. If the course says "auto-accept still asks before commands," also say why.
   - Break steps into numbered lists and options into bullets or tables.
   - Use a diagram when a process or flow is easier to see than to read.
   - **Draw diagrams in Mermaid** (a ` ```mermaid ` code block), never as plain-text or box-drawing art. GitHub turns Mermaid into a real picture.
     - A process or loop → `flowchart`
     - Who sends what to whom, step by step → `sequenceDiagram`, with one column per player
     - Where things live → `flowchart` with a `subgraph` for each place, such as "Your computer" and "Anthropic's servers"
   - Keep ` ```text ` blocks only for literal content: folder trees, command output, the exact text of a message.
   - When a lesson involves more than one player (you, Claude Code, your computer, the model, outside services), add a "Who's who" table first: where each one lives, what it does, and an example. Model: section 5 of `01_ClaudeCode101/02-how-claude-code-works.md`.
   - Make examples concrete: real file names, real file contents with line numbers, the exact command, and the exact output. Show what goes where, not just "it searches" or "it sends the result."

3. **Add examples where they help.**
   - Give a concrete example for each key idea, such as a sample prompt, a command, or a "for example, if a test fails..." case.
   - Keep examples realistic and short.

4. **Keep the course images.**
   - Images make lessons easier to understand. Every screenshot or diagram in the lesson should appear in the notes.
   - Save them in the course's `images/` folder as `0X-short-name.png` (for example, `images/03-login-method.png`) and embed them where they belong: `![What it shows](images/03-login-method.png)`.
   - If I paste the lesson text without its images, leave a marker where each image goes, such as `<!-- IMAGE: caption → images/03-name.png -->`, and ask me to paste the screenshots.

5. **Cover everything in the lesson.**
   - Every point in the transcript and course text must appear in the notes.
   - When the video and the written course differ, follow the written course and tell me what differed.
   - When you add something the course doesn't say, tell me which parts in your reply so I can check them.

6. **Always end with an FAQ.**
   - Questions as `**Q1. ...?**`, answer on the next line.
   - Cover every main idea in the lesson.
   - End with 1–2 `(Exam angle)` questions that connect the lesson to the exam domains.

## File layout

- Each course is one folder, such as `01_ClaudeCode101/`.
- Each lesson is one file directly in that folder: `0X-lesson-name.md`, numbered in course order. No chapter subfolders.
- Lesson images go in `images/` inside the course folder. This is the only subfolder.
- Each course folder has a `README.md` index. When a lesson is done, link it there and mark it ✅ Done.

## Lesson file structure

Follow `01_ClaudeCode101/02-how-claude-code-works.md`:

1. Title: `# Lesson N — Lesson name`
2. Header: the info line, then the navigation table (exact format below), then `---`
3. "On this page" table (format below), then `---`
4. The lesson content, in sections
5. `### Recap`
6. `## My notes / practice`: a checklist of hands-on things to try
7. `## FAQ`
8. Footer: `---`, then the **same** navigation table as the header

### Header and footer format

Use exactly this. Don't use a `>` blockquote for the header: GitHub joins its lines into one messy paragraph.

```markdown
# Lesson 2 — How Claude Code works

**Course:** [Claude Code 101](https://academy.claude.com/courses/claude-code-101) &nbsp;·&nbsp; **Chapter 1:** What is Claude Code? &nbsp;·&nbsp; **Completed:** October 17, 2026

| Previous | Course | Next |
|:---|:---:|---:|
| [← What is Claude Code?](01-what-is-claude-code.md) | [📚 Course index](README.md) | [Installing Claude Code →](03-installing-claude-code.md) |

---
```

- First lesson: put `Start of course` in the Previous cell.
- Last item: put `End of course` in the Next cell.
- When a new lesson is added, also check the previous lesson's Next link in both its header and footer.

### "On this page" table

Right after the header, add a table that jumps to each section of the page:

```markdown
**On this page**

| # | Section |
|:---:|:---|
| 1 | [In one sentence](#in-one-sentence) |
| 2 | [1. The loop: look, do, check, repeat](#1-the-loop-look-do-check-repeat) |
| 3 | [My notes / practice](#my-notes--practice) |
| 4 | [FAQ](#faq) |

---
```

- List every `##` and `###` heading in page order, including Recap, My notes / practice, and FAQ. Skip `####` subheadings.
- Use bold text for "On this page", not a heading, so the table doesn't list itself.
- Build each link the way GitHub does: lowercase, delete punctuation except hyphens, and turn each space into `-`. For example, `Where it's available` becomes `#where-its-available`, and `My notes / practice` becomes `#my-notes--practice`.
- If you rename, add, or remove a heading, update the table.
