# From Zero to Code: setting up Python

From Zero to Code:
Getting Started with Python and VS Code
Welcome to RUNI’s Introduction to Computer Science course! Three tools that will be used extensively in this course are Python, VS Code, and GitHub. Python is a powerful and widely used programming language; VS Code is a popular code editor that, with the right extensions, serves as an Integrated Development Environment (IDE) for many programming languages, including Python; GitHub is a cloud-based platform that helps developers store, share, and manage versions of their software. This document guides you through setting up Python and VS Code on your Mac or Windows computer; we’ll deal with GitHub later. Because you are a computer science student, we view this document not only as a technical guide but also as part of your computer science education.
Background
Python was created by the Dutch programmer Guido van Rossum and first released in 1991. It is named after the British comedy group Monty Python, not after the snake. Today, Python is open-source software, developed by a worldwide community and supported by the non-profit Python Software Foundation.
VS Code was developed by Microsoft, which made a wise decision to let people use it to develop programs in any language, including Python. This decision was consistent with Microsoft’s vision to build a global developers ecosystem. This is also why Microsoft bought the GitHub platform, which we will discuss and use later in the course.
Python, VS Code, and GitHub are freely available and can be used on almost any computer platform. Why are companies willing to invest money and resources in developing give-away software? That’s an interesting question that you are welcome to think about.
Installing Python
To run Python programs, you need the Python interpreter: a program that reads Python code and executes it, statement by statement. Behind the scenes, the interpreter first translates the code into a lower-level form called bytecode and then executes the bytecode. This happens automatically: unlike some other languages, Python has no separate compilation step for you to perform.
Install the latest stable version of Python: at the time of writing (October 2026), Python 3.15.0. If a newer 3.15 release (such as 3.15.1) is listed when you download, take the newest one.
Mac users (Apple Silicon or Intel): Go to the Python Releases for macOS page and, under the newest Python 3.15 release, click macOS installer. The same installer works on all Macs. Open the downloaded .pkg file and follow the installation steps, keeping the default options.
Windows users: Go to the Python Releases for Windows page and, under the newest Python 3.15 release, click Windows installer (64-bit), or Windows installer (ARM64) if your laptop has an ARM processor (see Settings > System > About > System type). Run the installer and, on its first screen, check the box Add python.exe to PATH before clicking Install Now. This setting lets you start Python by typing python in a terminal. (The same page also links to a Python install manager; this guide uses the standard installer instead.)
Once Python is installed, you’re all set. If VS Code was open during the installation, restart it so that it finds the new installation.
Installing VS Code
Download and install VS Code for your operating system from Microsoft’s VS Code page.
Locate VS Code in your computer’s applications folder, or use your OS search bar to find it. Launch (start executing) VS Code on your computer.
VS Code is designed for writing programs in many different programming languages. Before using it in our course, customize it to work with Python. To do so, click the sidebar’s Extensions icon, search for “Python”, and install the extension named Python by Microsoft. This extension, together with a few companion extensions installed along with it, adds Python support to VS Code: color-coded syntax, error detection, and tools for running and debugging programs.
Python program development: Writing and Running
0. Assumptions
We assume that you’ve installed Python, VS Code, and the Python extension.
In the first few weeks of the course, you will not write Python programs from scratch. Instead, we will give you skeletal programs (תכניות שלדיות) that you will have to complete. Each program, say MyProg, is stored in a separate file, say MyProg.py. Keeping files well organized is essential. In a nutshell, we use folders to keep together programs that have something in common. For example, all the programs that belong to Homework Assignment 1 are given in a folder named HW1. These programs are available on the course website in Moodle as a single compressed file named HW1.zip.
Create a folder named intro2cs on your computer. Download HW1.zip from the “Week 1” section on the course website and extract it into the intro2cs folder.
Next, start VS Code. All the operations described below are performed in VS Code.
1. Open the relevant folder
To start working on an existing program, open the folder where the program’s code is stored. For example, let’s open the folder intro2cs/HW1/code:
Select File > Open Folder;
Navigate to the intro2cs/HW1/code folder on your computer;
Click Open (on Windows: Select Folder) to load the folder’s files into VS Code.
The first time you open a folder, VS Code asks whether you trust the authors of its files. Click Yes, I trust the authors. Figure 1 shows how to open a folder on a Mac.

Figure 1. Opening the intro2cs/HW1/code folder from VS Code’s Welcome page (Mac).
2. Select a file to work on
Once a folder has been opened in VS Code, its files appear in the sidebar pane that VS Code calls Explorer. Click the file you want to work on. For example, if you wish to edit the Demo0 program, click the file name Demo0.py.
3. Open a new terminal session
The terms “terminal”, “command prompt”, and “shell” are used on different platforms to describe the same thing: an interactive program that lets developers manage files and run programs by typing textual commands. The names of these commands are cryptic and telegraphic. For example, the command ls lists the files in the current folder, and pwd prints the path of the current folder (in Unix, folders are called directories). There are numerous such commands, but for the purpose of this course, you need to know only a few of them.
VS Code has a built-in terminal, which is accessed as follows:
Click Terminal > New Terminal.
A terminal pane will open at the bottom of the VS Code window, in the folder you opened in step 1. On a Mac, the terminal runs a shell named zsh; on Windows, it runs PowerShell.
As a sanity check, type the following command in the terminal and press Enter:
Mac: python3 --version
Windows: python --version
If the terminal responds with Python 3.15.0 (or a newer 3.15 release), Python was installed successfully on your computer. If you get a different version or an error message:
Mac: Quit VS Code completely (⌘+Q), start it again, open a new terminal, and repeat the check. If the problem persists, run the Python installer again.
Windows: If python opens the Microsoft Store or is “not recognized”, the Add python.exe to PATH box was probably left unchecked. Run the installer again, choose Uninstall, and then install Python again, this time with the box checked. Restart VS Code and repeat the check.
4. Editing
To edit a file, use the VS Code editor, which provides color-coded syntax, helpful editing hints, and syntax error detection. To practice editing, locate in the loaded file the statement i = 0. Just below it, enter the new statement print(i). Make sure that print(i) starts at exactly the same column as i = 0. In Python, indentation (the spaces at the beginning of a line) is part of the syntax: a misaligned statement either causes an error or changes the program’s meaning.
To save your edits, click File > Save (or press Ctrl+S on Windows or ⌘+S on Mac). Curiously, VS Code does not feature a traditional file-save icon.
5. Running
To run Demo0.py, enter the following command in the terminal:
Mac: python3 Demo0.py
Windows: python Demo0.py
This command starts the Python interpreter and applies it to the file Demo0.py. The interpreter executes the program, and you will see on the screen what the program is supposed to do; thanks to the statement you added, the output will include the number 0.
If the program has a syntax error, the interpreter reports it, including the line number, and runs nothing. Other errors, such as an attempt to divide by zero, are detected only when the offending statement is reached; these are called runtime errors.
Curiously, on a Mac the command is python3, not python: a convention from the years when Macs came with the older Python 2 preinstalled as python.
Alternatively, click the Run Python File button (the triangle at the top-right corner of the editor). It uses the Python version shown in the status bar at the bottom of the window; if that version is not 3.15, click it and select Python 3.15.
Did you manage to run your first Python program?
If so, Mazal Tov! You made the first step in your software developer journey.
If you encounter errors and problems along the way, don’t worry. You just joined the millions of developers who struggle with software bugs at any given moment on this planet. So, welcome to the club! During the first week of the course, we’ll discuss installation problems and debugging and help you sort them out. If you need assistance, post a question in the Week 1 Q&A forum on the course website or raise it during the first week’s workshop (סדנה). Remember: troubleshooting is a key part of learning, so don’t hesitate to ask for help!
