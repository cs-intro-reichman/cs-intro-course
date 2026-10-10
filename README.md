# CS Intro Course: AI Tutor

An AI tutor for the Reichman University course **Introduction to Computer Science (Python)**. You install it in [Claude](https://claude.ai). After that, Claude knows the course material and helps you the way a teaching assistant would.

**[⬇ Download the tutor (cs1-python-tutor.zip)](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor.zip)**

## What it does

- Explains any lecture topic using the course's own examples and terminology, and points you to the relevant slide.
- Helps you understand error messages and find bugs in your code.
- Helps you prepare for the exam: explains topics, asks practice questions and checks your answers.
- Only uses Python that the course has taught up to that week.
- Answers in the language you write in (English or Hebrew).

## What it doesn't do

It doesn't write solutions to homework. For homework it guides you step by step: it asks leading questions, points you to the relevant material, and gives feedback on code you wrote yourself. That way you learn to solve problems on your own, which is what you'll need in the exam, where there's no AI.

## Installing (once, about 2 minutes)

1. Download [cs1-python-tutor.zip](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor.zip). **Don't unzip it.**
2. Open [claude.ai](https://claude.ai) or the Claude desktop app. Any plan works, including Free.
3. Go to **Settings → Capabilities** and turn on **Code execution and file creation**.
4. Go to **Customize → Skills**, click **+**, then **Create skill**, then **Upload a skill**, and choose the zip file.
5. Make sure the skill's toggle is on.

## Using it

You don't need to turn anything on. Open a new chat and ask as usual, for example:

- "I don't understand what return does"
- "Why does my code print 0?" (and paste your code)
- "What's the difference between a list and a tuple?"
- "Give me practice questions on dictionaries"

## Updating

New material (lectures, homework assignments) is added during the semester, and each time there's a new version of the tutor. The current version is the date in [`VERSION`](VERSION). You need to reinstall to get it, because Claude doesn't update skills by itself.

**When to reinstall:**
- The course staff announces a new version, or the date in `VERSION` is newer than yours.
- The tutor tells you that a topic or a homework assignment isn't in its material yet.

**To check which version you have,** ask the tutor: "Which version of the course tutor is this?"

## Reinstalling (Claude)

1. Download the latest [cs1-python-tutor.zip](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor.zip). Don't unzip it.
2. In Claude, go to **Customize → Skills** and find **cs1-python-tutor**.
3. Turn its toggle off, then open the **...** menu next to the toggle and choose **Delete**.
4. Click **+**, then **Create skill**, then **Upload a skill**, and choose the new zip.
5. Make sure the new skill's toggle is on.
6. Start a **new chat**. A chat you opened before reinstalling may still use the old version.

If the upload fails with a message that the skill already exists, the old one wasn't deleted: go back to step 3.

## Using another AI (ChatGPT, Gemini)

The tutor works best in Claude, where it switches on by itself whenever you ask about the course. If you prefer ChatGPT or Gemini, you can set it up there as a custom assistant. Two differences:
- It works only inside that assistant. Open the Gem, GPT or project whenever you want course help.
- Updates are manual: when a new version comes out, follow [Reinstalling in ChatGPT or Gemini](#reinstalling-in-chatgpt-or-gemini).

**Step 1 (for both):** download [cs1-python-tutor-portable.zip](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor-portable.zip) and **unzip it**. Inside you'll find:
- `INSTRUCTIONS.txt`: the tutor's instructions. You'll copy its whole text.
- `knowledge/`: 7 files with the course material. You'll upload all of them.

### Gemini: create a Gem

1. Open [gemini.google.com](https://gemini.google.com) and sign in.
2. In the left sidebar, open **Gems** (or **Explore Gems**) and click **New Gem**.
3. **Name:** `CS Intro Tutor`.
4. **Instructions:** open `INSTRUCTIONS.txt`, copy all of its text, and paste it into the instructions box.
5. **Knowledge:** click the **+** (add files) button and upload all the files from the `knowledge` folder.
6. Click **Save**.
7. To use it, choose **CS Intro Tutor** from the Gems list in the sidebar and chat as usual.

### ChatGPT: create a GPT

Creating a GPT may require a paid ChatGPT plan. On the free plan, use a project instead (next section).

1. Open [chatgpt.com](https://chatgpt.com) and sign in.
2. In the sidebar, click **GPTs**, then **+ Create**.
3. Switch to the **Configure** tab.
4. **Name:** `CS Intro Tutor`.
5. **Instructions:** paste the whole text of `INSTRUCTIONS.txt`.
6. **Knowledge:** click **Upload files** and upload all the files from the `knowledge` folder.
7. Click **Create** and choose **Only me**.
8. To use it, open **CS Intro Tutor** from the sidebar and chat as usual.

### ChatGPT: use a project (works on the free plan)

1. In the ChatGPT sidebar, click **New project** and name it `CS Intro Tutor`.
2. Open the project's settings (the **...** menu next to its name, or the **Instructions** option inside the project) and paste the whole text of `INSTRUCTIONS.txt` as the project's instructions.
3. Click **Add files** and upload the files from the `knowledge` folder. If your plan allows fewer files, upload `course-map.md`, `python-taught.md` and the lecture file for the weeks you're studying now.
4. Start every course chat inside this project.

### Reinstalling in ChatGPT or Gemini

1. Download the latest [cs1-python-tutor-portable.zip](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor-portable.zip) and unzip it.
2. Open your Gem, GPT or project for editing:
   - **Gem:** in Gemini, open the Gems list, then the **...** menu next to **CS Intro Tutor**, then **Edit**.
   - **GPT:** in ChatGPT, open **GPTs**, then **My GPTs**, then the edit (pencil) button next to **CS Intro Tutor**.
   - **Project:** open the project and its settings or files.
3. Replace the instructions: delete all the old text and paste the whole text of the new `INSTRUCTIONS.txt`.
4. Remove all the old knowledge files, then upload all the files from the new `knowledge` folder. Don't keep the old files next to the new ones: the assistant could read outdated material.
5. Save (in a GPT, click **Update**), and start a new chat.

## What's in this repository

| | |
|---|---|
| `cs1-python-tutor.zip` | The file you upload to Claude (always the latest version). |
| `cs1-python-tutor-portable.zip` | The same tutor for ChatGPT and Gemini (instructions + course files). |
| `cs1-python-tutor/` | The same skill, unpacked, if you want to see what's inside. |
| `VERSION` | The current version and which lectures it includes. |
