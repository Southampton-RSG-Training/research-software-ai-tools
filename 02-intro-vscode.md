---
title: "Introduction to Microsoft Visual Studio Code"
teaching: 25
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do I access the key features of Microsoft Visual Studio (VS) Code?
- How do I open a software project in VSCode?
- What are VSCode extensions, and how do I use them?
- What editing features will help me when writing code?
- How do I run code in VSCode?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Describe the general layout of the VSCode interface
- Download or clone an existing remote GitHub repository
- Open a code folder in VSCode using the explorer feature
- Install and configure an extension to VSCode that helps with Python code development
- Use syntax highlighting to identify code styling issues and common coding mistakes
- Use code completion to automate finishing an incomplete code statement
- Describe how VSCode highlights the status of files managed under version control
- Use VSCode to run a Python script and have any text output displayed within a terminal

::::::::::::::::::::::::::::::::::::::::::::::::

This session provides an introduction to Integrated Development Environments (IDEs), powerful tools for software development. We will explore how various features built into IDEs can streamline your software development workflow, 
especially through their built-in debugging tools — which allow you to identify and fix issues with your code efficiently. 

## Introduction to IDEs

### What is an Integrated Development Environment (IDE)?

An Integrated Development Environment (IDE) is a graphical application that provides a comprehensive workspace for writing, editing, testing, and debugging code—all in one place. 
At the core of an IDE is a code editor, and it combines several tools that developers need into a single interface to streamline the code development process. 
IDEs are extremely useful and modern software development would be very hard without them. 

Historically, developers typically wrote code using simple text editors, often terminal-based with no graphical interface or syntax checking support. 
They had to rely on separate tools outside the editor to compile, debug, and manage their code, making development a much more fragmented experience. 
It is worth noting that popular terminal-based editors such as Emacs and Vim may appear deceptively simple at first glance - but they are, in fact, highly 
powerful and customisable frameworks for coding and automating development workflows.

Today, although some IDEs are designed for specific programming languages, many modern IDEs can support multiple languages through a wide variety of plugins — often created and maintained by the developer community.

### Why use an IDE?

An IDE brings everything you need to write, test, and debug code into one place — saving time by helping you write better code faster.
IDEs help by:

- reducing setup and development time - everything you need for editing, running, and debugging code is in one place and the need to switch between different tools/applications/windows is significantly reduced
- offering helpful tools like syntax checking, code suggestions and autocomplete, and error checking leading to fewer errors thanks to real-time feedback and intelligent suggestions
- making it easier to debug and test code leading to easier issue detection and fixing
- providing a consistent environment across projects

For beginners, IDEs lower the barrier to entry by making it easier to spot mistakes and understand code structure. 
For experienced developers, IDEs boost productivity and streamline complex workflows.

### Common IDE Features

Let’s look at what most IDEs offer - these features all work together to make your life easier when coding:

- Code editor with syntax highlighting and automatic code formatting for better readability and consistency
- Intelligent code completion that suggests syntactically correct options as you type to speed up development
- Powerful search tools to quickly locate functions, classes, or variables
- Inline documentation and reference lookup to understand symbols (functions, parameters, classes, fields, and methods) and variables definitions and usage without leaving your code
- Built-in support for running and managing tests through integrated testing frameworks
- Seamless integration with version control systems (like Git) for tracking changes and collaboration
- Debugging tools for setting breakpoints, stepping through code, and inspecting variables during runtime
- An integrated terminal for executing commands directly within the IDE
- A project/file explorer for easy navigation and management of your software project
- Viewing various files in different file formats (CSV, JSON, YAML, images, HTML, etc.) that are part of your software project 

Some IDEs also offer: 

- Deployment tools to package and release your code efficiently
- Basic project and issue tracking features to support task management

### Popular IDEs
  
Here are a few widely used IDEs across different languages and fields:

- [Visual Studio Code (VS Code)][vs-code] – lightweight and highly customisable; supports many languages
- [PyCharm][pycharm] – great for Python development
- [RStudio][r-studio] – tailored for R programming but allows users to mix (R Markdown) text with code in R, Python, Julia, shell scripts, SQL, Stan, JavaScript, C, C++, Fortran, and others, similar to Jupyter Notebooks.
- [Eclipse][eclipse] – often used for Java and other compiled languages
- [JupyterLab][jupyter-lab] – interactive environment for Python and data science
- [Spyder][spyder] – popular among scientists using Python

## Getting Started with VSCode

Let's start by running VSCode now on our machines, so run it now.
How you run VSCode will differ depending on which operating system you have installed.

The first thing you'll likely see is a welcome-style page with links to features for opening files, and creating or opening a project.
You may find it asks you which kind of theme you'd like - you can select from either a dark or light theme.

### Navigating Around VSCode

So let's take a look at the application.
You'll see some icons on the left side, which give you access to its key features.
Hovering your mouse over each one will show a tooltip that names that feature:

![](fig/vscode-overview.png){alt='Screenshot of VSCode interface' .image-with-shadow width="100%" }

- `Explorer` - the top one is a file navigator, or explorer - we can use this to open existing folders containing program files.
- `Search ` - the next one down is a search capability, so you can search for things (and replace them with other text) over your code files.
- `Source control` - this gives you access to source code control, which includes Git version control functionality. This feature means you can do things like clone Git repositories (for example, from GitHub), add and commit files to a repository, things like that.

  ::::::::::::::::::::::::::::::::: callout
    
  If you're not familiar with Git, that's totally fine - you don't have to use this feature, although it's worth looking into using version control for writing your code.
  Version control Systems like Git allow you to manage your code by storing it - and all the changes you make to it - within a repository hosted elsewhere, for example, on GitHub.

  :::::::::::::::::::::::::::::::::::::::::

- `Run and Debug` - this allows you to run programs you write in a special way with a debugger, which allows you to check the state of your program as it is running, which is very useful and we'll look into later.
- `Extensions` - which we'll look into right now, allows you to install extensions to VSCode to extend its functionality in some way.

At the very bottom of the main VSCode window is the `Status bar`, which shows us 

There are many other features and ways to access them, and we'll cover key ones throughout this lesson.

### Installing Extensions

Extensions are a major strength of VSCode. Whilst VSCode appears quite lightweight, and presents a simple interface (particularly compared to many other IDEs!), this is quite deceptive.
You can extend its functionality in many different ways. 
For example, installing support for other languages, greater support for version control, there's even support for working with databases, and so on.
There are literally tens of thousands of possible extensions now.

Now VSCode already comes with built-in support for JavaScript, including TypeScript and node.js,
but also has extensions for other languages too (C++, C#, Java, PHP, Go, and many others).
Installing a language extension will allow you to do more things with that particular language in VSCode, as we'll see now.

Let's install an extension now:

1. Firstly, select the extensions icon, then type in "Python" into the search box at the top, and it'll give you a list of all Python-related extensions.
1. Select the one which says `Python` from Microsoft. This is the Microsoft official Python extension.
1. Then select `Install`.

It might take a minute - you can see a sliding blue line in the top left to indicate it's working.

::::::::::::::::::::::::::::::::::::::::: instructor

## Checkpoint: who's successfully managed to install the Python extension?

::::::::::::::::::::::::::::::::::::::::: 

Once complete, you should see a couple of "Welcome" windows introducing you to two of its key features - support for Python and Jupyter notebooks.
If you use Jupyter notebooks, which is a way of writing Python programs that you can run line by line from within an editor as you write the program, you may find this useful.

For now, let's configure this extension for our Python development, and to do that, we need to tell VSCode which Python installation on our machine we'd like it to use. VSCode has a sophisticated method to access it's inner functionality known as the Command Palette, which we'll use to address this.

1. Select `View` and `Command Palette` from the VSCode menu
1. Begin typing `Python: Select Interpreter`, and then select it when it appears
1. A list of available Python installations should appear. You may find you have many installations of Python, or only have one. Try to select the version later than 3.8 if you can.

Once selected, the default Python interpreter for VSCode will be configured.

::::::::::::::::::::::::::::::::::::::::: instructor

## Checkpoint: who's configured the Python extension?

::::::::::::::::::::::::::::::::::::::::: 

### A Sample Project

Next, let's obtain some example Python and edit it from within VSCode.
First, download the example code we'll use from FIXME, either as a `.zip` or `.tar.gz` compressed archive file.
If you're unsure, download the `.zip` file.
Then, extract all the files from the archive into a convenient location.
You should see files contained within a new directory named `FIXME`.

Now we need to load the code into VSCode to see it. You can do this in a couple of ways, either:

1. Select the `Source control` icon from the middle of the icons on the left navigation bar. You should see an `Open Folder` option, so select that.
1. Select the `File` option from the top menu bar, and select `Open Folder...`.

In either case, you should then be able to use the file browser to locate the directory with the files you just extracted, and then select `Open`.
Note that we're looking for the *folder* that contains the files, not a specific file.

::::::::::::::::::::::::::::::::: callout

## What about using Git Version Control?

If your system has the Git version control system installed, you may see a `Clone Repository` option here too.
If you are familiar with Git and wish to use this option instead,
select it and enter the repository's location as `FIXME`.
Then use the file browser that is presented to find a convenient location to store the cloned code and click on `Select as Repository Destination`,
then select `Open` when ‘Would you like to open the cloned repository?' popup appears.

:::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: instructor

## Checkpoint: who's been able to download the code and open it within VSCode?

::::::::::::::::::::::::::::::::::::::::: 

You may be presented with a window asking whether you trust the authors of this code.
In general, it's a good idea to be at least a little wary, since you're obtaining code from the internet, so be sure to check your sources!
Be careful here - I found on Windows the "Trust" option appears on the left, whilst on Mac, it appears on the right!
In this case, feel free to trust the repository!
You'll then see the explorer present you with some files in a small window (or pane) on the left you can use to navigate and find files.

So far within VSCode we have downloaded some code from a repository and opened a folder.
Whenever we open a folder in VSCode, this is referred to as a "Workspace" - essentially, a collection of a project's files and directories.
So within this workspace, you'll see the following:

FIXME: list of files in file explorer

## Using VSCode

Now we've acquainted ourselves with running VSCode, let's take a look at our example code.
Select the `FIXME` file in the explorer window, which will bring up the contents of the file in the code editor.

::::::::::::::::::::::::::::::::: callout

## The File Explorer has Disappeared!

You may find, perhaps on reopening VSCode, that the explorer is no longer visible.
In this case, you can select `Explorer` from the sidebar to bring it back up again,
and if you don't currently have a workspace loaded,
you can select `Open Folder` to select the code folder.

:::::::::::::::::::::::::::::::::::::::::

Note that as an example, the code is deliberately written to have flaws.
Things like the line spacing is inconsistent, there are no code comments, there's a variable that's not used, and you may spot other issues too.
But in essence, the code is designed to do the following:

1. Open a file in the CSV (comma separated value) format
1. Go through the file line by line, and:
   - If the line begins with a `#` symbol, ignore it.
   - Otherwise, extract the fourth column (which contains temperature in Fahrenheit), convert it to Celsius and Kelvin, and output those readings.

Let's take a look at some of what the code editor gives us.

### Syntax Highlighting

You'll notice that the Python syntax is being highlighted for us, which helps readability.

Here, it uses colour to distinguish the various parts of our program.
Functions are yellow, Python statements are purple, variables are light blue, and strings are this reddy-orange, and so on.
Which, perhaps unsurprisingly, is a feature known as Syntax Highlighting, and it's possible to edit the colour scheme to your liking for a particular language if you like, although we won't go into that now.

This is really handy to give you immediate feedback on what you are typing, and can help you to identify common syntax mistakes.
For example, deleting the closing parenthesis on `open` - the opening one goes red, with a squiggly line underneath, indicating an issue.

So this is great, and helps us understand what we are writing, and highlights some mistakes.

### Code Completion

Something that's also useful is VSCode's ability (via the Python and Pylance extensions) to help you write and format your code whilst you're typing.

For example, on a blank line somewhere, enter `for x in something:`, and press the enter (or return) key.

On the next line, we can see that it's automatically indented it for us, knowing that we're inside a loop.

Another really helpful feature is something known as code completion (in VSCode, this is referred to as IntelliSense).
This is a great time saver, and a really useful feature of IDEs.
Essentially, as you type, it works out the context of what you are doing, and gives you hints.

FIXME: adapt below to example code used

For example, if we start typing a variable we've already defined, for example `climate_data`,
we can see that it's zeroing in as we type on the options for what we might be trying to type.
When we see `climate_data`, we can press `Tab` to complete it for us.
As another example, if we wanted to open another file, we might type `new_file = open(`.
In this case, it provides information on the file `open` function and its arguments, along with a description of what it does.
This is really handy to we don't have to take the time to look up all this information up on the web, for example.

::::::::::::::::::::::::::::::::: callout

### Using a Git Code Repository?

For those of you familiar with version control and who retrieved the example code via cloning its repository instead of downloading it, there are some other editor features that help with using version control.
One of these is that the filename changes colours in the file explorer depending on its status within version control:

- White - an existing file is unchanged from the copy in the local repository).
- Orange - the content of an existing file has changed, and the change(s) have not been tracked by version control yet.
- Green - a new file has been added and is unknown to version control.

So at a glance, you can get an idea of what's changed since your last commit.

:::::::::::::::::::::::::::::::::::::::::

### Summary

So in summary, many of these editing features are typical of IDEs in general,
and the great thing is that they are really helpful at saving us time.
Things like syntax highlighting, code completion, automatic code formatting and inserting docstrings, may not seem like much, but it all adds up!

## Running Python in VSCode

Now let's try running a Python script.
First, make sure your Python code doesn't have any errors!
Then, select the "Play"-looking icon at the top right of the code editor.

You should see the program run, and output displayed in a pop-up terminal window at the bottom:

FIXME: adapt to show output from updated example

```output
steve@laptop:~/code-style-example$ /bin/python3 /home/steve/code-style-example/climate_analysis.py
Max temperature in Celsius 14.73888888888889 Kelvin 287.88888888888886
Max temperature in Celsius 14.777777777777779 Kelvin 287.92777777777775
Max temperature in Celsius 14.61111111111111 Kelvin 287.76111111111106
Max temperature in Celsius 13.838888888888887 Kelvin 286.9888888888889
Max temperature in Celsius 15.477777777777778 Kelvin 288.62777777777774
Max temperature in Celsius 14.972222222222225 Kelvin 288.1222222222222
Max temperature in Celsius 14.85 Kelvin 288.0
Max temperature in Celsius 16.33888888888889 Kelvin 289.4888888888889
Max temperature in Celsius 16.261111111111113 Kelvin 289.4111111111111
Max temperature in Celsius 16.33888888888889 Kelvin 289.4888888888889
steve@laptop:~/code-style-example$ 
```

::::::::::::::::::::::::::::::::::::::::: instructor

## Checkpoint: who's run their Python progran and seen some output in a pop-up window?

::::::::::::::::::::::::::::::::::::::::: 

::::::::::::::::::::::::::::::::: callout

## Error: `the term conda is not recognised`

If you're running an Anaconda distribution of Python on Windows,
if you see this error it means that VSCode is not looking in the right place for Anaconda's installation.
In this case, you may need to configure VSCode accordingly:

1. Activate the Command Palette, either by selecting `View` and `Command Palette` in the menu, or by pressing `Ctrl` + `Shift` + `P` (Linux), `Mac/Windows Key` + `Shift` + `P` (Mac/Windows) simultaneously
1. Type `Terminal: Select Default Profile`
1. From the options, select the entry that's something like `Command Prompt C:\WINDOWS\...`

Hopefully that should resolve the issue.

::::::::::::::::::::::::::::::::::::::::: instructor

## Checkpoint: if you're using Conda and encountered this error, did it fix it?

::::::::::::::::::::::::::::::::::::::::: 

:::::::::::::::::::::::::::::::::::::::::

The pop-up window is known as the "Console" or "Terminal",
and essentially is a terminal, or command prompt, where the program is run.
You'll notice that the directory where the console runs is the current VSCode project's workspace location,
and that we can also type in commands here too.
For example in Windows, you could type `dir`, on Mac or Linux you could type `ls` - to get a listing of files, for example.

We can also close this terminal/console at any time by selecting the `x` icon on the right,
and start a new one by selecting `Terminal` from the menu and selecting `New Terminal`.
So when we write and run our code, we have the option of never having to leave VSCode at all for most things.


::::::::::::::::::::::::::::::::::::: keypoints 

- Integrated Development Environments (IDEs) are all-in-one tools for writing, editing, testing, and debugging code, improving developer efficiency by reducing the need to switch between different applications
- Key VSCode features are accessible via the left navigation bar and the menu
- VSCode's capabilities can be increased by installing extensions
- A VSCode "workspace" is a project that consists of a collection of folder and files
- Git source code repositories on GitHub can be cloned locally and opened from within VSCode
- Syntax highlighting gives you immediate feedback of potential issues as you write code
- Code completion helps to automatically finish incomplete code statements and names
- Run a script by selecting the "Play" icon in VSCode
- Output from running a Python script is displayed in the interactive "console" or "terminal"

::::::::::::::::::::::::::::::::::::::::::::::::
