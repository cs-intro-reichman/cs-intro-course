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

New material is added during the semester. If you ask about a topic that isn't in your version yet, the tutor will tell you. That's the sign to update:

1. Download the latest zip from this page.
2. In **Customize → Skills**, open the **...** menu next to the old skill and choose **Delete**.
3. Upload the new zip, the same way you installed it.

## What's in this repository

| | |
|---|---|
| `cs1-python-tutor.zip` | The file you upload to Claude (always the latest version). |
| `cs1-python-tutor/` | The same skill, unpacked, if you want to see what's inside. |
| `VERSION` | The current version and which lectures it includes. |
