# CS Intro Course: AI Tutor

An AI tutor for the Reichman University course **Introduction to Computer Science (Python)**. You install it in [Claude](https://claude.ai). After that, Claude knows the course material and helps you the way a teaching assistant would.

**[⬇ Download the tutor (cs1-python-tutor.zip)](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor.zip)**

<div dir="rtl">

## מה זה?

מורה פרטי מבוסס AI לקורס **מבוא למדעי המחשב (Python)** באוניברסיטת רייכמן. מתקינים אותו ב-[Claude](https://claude.ai), ומאותו רגע Claude מכיר את חומר הקורס ועוזר לכם כמו מתרגל.

**מה הוא עושה:**
- מסביר כל נושא מההרצאות, עם הדוגמאות והמונחים של הקורס, ומפנה לשקף הרלוונטי.
- עוזר להבין הודעות שגיאה ולמצוא באגים בקוד שלכם.
- עוזר להתכונן למבחן: מסביר, שואל שאלות תרגול ובודק את התשובות שלכם.
- משתמש רק ב-Python שכבר נלמד בקורס עד אותו שבוע.
- עונה בשפה שבה פניתם אליו, עברית או אנגלית.

**מה הוא לא עושה:** הוא לא כותב פתרונות לתרגילי בית. בשיעורי בית הוא עוזר צעד אחר צעד: שואל שאלות מכוונות, מפנה לחומר הרלוונטי ונותן משוב על הקוד שאתם כותבים. כך אתם לומדים לפתור לבד, וזה מה שתצטרכו במבחן, שבו אין AI.

## התקנה (פעם אחת, כ-2 דקות)

1. הורידו את [cs1-python-tutor.zip](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor.zip). **אל תפתחו את ה-zip.**
2. היכנסו ל-[claude.ai](https://claude.ai) או לאפליקציית Claude במחשב. מתאים לכל תוכנית, כולל החינמית.
3. **Settings → Capabilities**: הפעילו את **Code execution and file creation**.
4. **Customize → Skills**: לחצו **+**, אחר כך **Create skill**, ואז **Upload a skill**. בחרו את קובץ ה-zip.
5. ודאו שהמתג של ה-skill דלוק.

## שימוש

אין צורך להפעיל שום דבר. פותחים צ'אט חדש ושואלים כרגיל, למשל:
- "לא הבנתי מה עושה return"
- "למה הקוד שלי מדפיס 0?" (והדביקו את הקוד)
- "תסביר לי את ההבדל בין רשימה ל-tuple"
- "תן לי שאלות תרגול על מילונים"

## עדכונים

חומר חדש נוסף לאורך הסמסטר. כשתשאלו על נושא שעוד לא נמצא בגרסה שלכם, המורה יגיד לכם, וזה סימן לעדכן:
1. הורידו מכאן את קובץ ה-zip העדכני.
2. ב-**Customize → Skills**, ליד ה-skill הישן: תפריט **...**, ואז **Delete**.
3. העלו את הקובץ החדש כמו בהתקנה.

</div>

## In English

**What it does:** explains any lecture topic using the course's own examples and slides, helps you understand error messages and find bugs, and helps you prepare for the exam. It only uses Python that the course has taught so far, and it answers in Hebrew or English, whichever you write in.

**What it doesn't do:** it won't write solutions to homework. For homework it guides you step by step, with leading questions, pointers to the material, and feedback on code you wrote yourself.

**Install (once):**
1. Download [cs1-python-tutor.zip](https://github.com/cs-intro-reichman/cs-intro-course/raw/main/cs1-python-tutor.zip). Don't unzip it.
2. Open [claude.ai](https://claude.ai) or the Claude desktop app. Any plan works, including Free.
3. **Settings → Capabilities**: turn on **Code execution and file creation**.
4. **Customize → Skills**: **+** → **Create skill** → **Upload a skill**, and choose the zip.
5. Make sure the skill's toggle is on.

Then just ask Claude your questions as usual in a new chat.

**Updating:** when the tutor says a topic isn't in its material yet, download the latest zip from this page, delete the old skill (**...** → **Delete**) and upload the new one.

## What's in this repository

| | |
|---|---|
| `cs1-python-tutor.zip` | The file you upload to Claude (always the latest version). |
| `cs1-python-tutor/` | The same skill, unpacked, if you want to see what's inside. |
| `VERSION` | The current version and which lectures it includes. |
