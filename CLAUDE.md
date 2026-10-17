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
2. Header block: course link and chapter, completed date, and Previous / Course index / Next links
3. The lesson content, in sections
4. `### Recap`
5. `## My notes / practice`: a checklist of hands-on things to try
6. `## FAQ`
