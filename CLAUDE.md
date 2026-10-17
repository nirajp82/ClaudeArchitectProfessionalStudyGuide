# Study guide rules

This repo holds my study notes for the Claude Architect Professional exam. These rules apply to every lesson note, every time.

## Writing lesson notes

The transcript and course text I paste are **reference only**. They tell you what the lesson covers. Don't just tidy them up. Put in extra effort so a beginner understands each idea on the first read.

1. **Use plain English.**
   - Short sentences. One idea per sentence.
   - Define every technical term the first time it appears, such as "a tool call is a request for Claude Code to do something."
   - No marketing words or filler.

2. **Make it clear, not just shorter.**
   - Explain *why*, not only *what*. If the course says "auto-accept still asks before commands," also say why.
   - Break steps into numbered lists and options into bullets or tables.
   - Use a diagram when a process or flow is easier to see than to read.

3. **Add examples where they help.**
   - Give a concrete example for each key idea, such as a sample prompt, a command, or a "for example, if a test fails..." case.
   - Keep examples realistic and short.

4. **Cover everything in the lesson.**
   - Every point in the transcript and course text must appear in the notes.
   - When the video and the written course differ, follow the written course and tell me what differed.
   - When you add something the course doesn't say, tell me which parts in your reply so I can check them.

5. **Always end with an FAQ.**
   - Questions as `**Q1. ...?**`, answer on the next line.
   - Cover every main idea in the lesson.
   - End with 1–2 `(Exam angle)` questions that connect the lesson to the exam domains.

## File layout

- Each course is one folder, such as `01_ClaudeCode101/`.
- Each lesson is one file directly in that folder: `0X-lesson-name.md`, numbered in course order. No chapter subfolders.
- Each course folder has a `README.md` index. When a lesson is done, link it there and mark it ✅ Done.

## Lesson file structure

Follow `01_ClaudeCode101/01-what-is-claude-code.md`:

1. Title: `# Lesson N — Lesson name`
2. Header block: course link and chapter, completed date, and Previous / Course index / Next links
3. The lesson content, in sections
4. `### Recap`
5. `## My notes / practice`: a checklist of hands-on things to try
6. `## FAQ`
