---
title: "Getting Started with using Copilot within VSCode"
teaching: 15
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do I use Copilot from within Visual Studio Code?
- How can I improve the relevance of responses from Copilot for my project?
- How much of my Copilot quota have I used?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Install and configure Visual Studio Code extension for Copilot
- Obtain answers to questions about how existing code works using Copilot's natural language chat
- Obtain suggestions on how to improve a codebase from Copilot
- Personalise Copilot suggestions to match project technologies and coding standards
- Determine Copilot usage within the free tier

::::::::::::::::::::::::::::::::::::::::::::::::

In this episode we'll look at installing and setting up Copilot within Visual Studio Code,
so we can use it with our example project,
and explore some basic features along the way.

## Install VSCode Copilot Extension

Extensions are a major strength of VSCode.
Whilst VSCode appears quite lightweight, and presents a simple interface (particularly compared to many other IDEs!), this is quite deceptive.
You can extend its functionality in many different ways. 
For example, installing support for other languages, greater support for version control, there's even support for working with databases, and so on.
There are literally tens of thousands of possible extensions now.

You may remember when you opened VSCode for this project there was a "Build with Agent" panel on the right.
This is the main chat interface to Copilot.
But in order to use it (and other Copilot features) we need to install an extension first:

1. Firstly, select the extensions icon, then type in "Copilot" into the search box at the top, and it'll give you a list of all Copilot-related extensions.
1. Select the one which says `GitHub Copilot` from Microsoft, which is the Microsoft official Copilot extension. You may also see the `GitHub Copilot Chat` extension, which will be automatically installed along with this one.
1. Select `Install`. It might take a minute - you can see a sliding blue line in the top left to indicate it's working.
1. You'll be presented with a "Welcome" page for the extension which covers the main features. Select `Mark Done`.

Now we have the extension installed, but we need to associate it with our GitHub account by signing in:

1. Select the `Signed out` button in the bottom right of the VSCode status bar, and `Sign in to use AI Features`.
1. Select `Continue with GitHub`.
1. You'll be redirected to a GitHub login web page to authorise Visual Studio Code for GitHub. Select the GitHub account you wish to use and select `Continue`.
1. Peruse and select `Authorize Visual-Studio-Code`.
1. You may need to further authenticate with GitHub authorise this action.
1. If a pop-up appears in your browser to open a link within VSCode, select `Open Link`.

Once completed, you'll now be able to use GitHub Copilot within VSCode.

## Asking Questions about Your Code

Attempting to understand a new codebase, whether it's your first week on a project or one you have inherited from another source, can be difficult. 
This can be due to many reasons; documentation may be incomplete, architectural decisions may be undocumented,
and the people who know the system may be unavailable or have left the organisation.

We can use Copilot to build our understand and confidence about our codebase by asking natural-language questions about the code. It helps you:

- Build a high-level mental model of the system, which with complex codebases is often a huge task!
- Identify where key functionality is located in the code
- Understand naming conventions, patterns, and dependencies
- Reduce the cognitive load of first contact with unfamiliar code

Which sounds great, but with one critical caveat:
it's important to understand that Copilot is not an absolute source of truth,
but more of a guide to help build your own understanding of a codebase.

Let's use Copilot to help us investigate how our existing codebase works.

### Using Copilot for the First Time

Let's move over to using the VSCode pane on the right, labeled `Build with Agent`.
You'll notice at the bottom there's a "chat" box,
with a number of selectable dropdown options below it.
You can hover over each one to discover what it is.

On the left, there's `Set Agent`, which allows you to set the mode of operation with Copilot.
Each of these modes provides an increasing degree of autonomy for Copilot to interact with your code:

- `Ask` - designed for learning and orienting yourself with existing code without changing it.
- `Edit` - proposes concrete code changes for your approval based on your instructions. It's useful when you already understand a codebase that you want to change.
- `Agent` - the most powerful mode, which lets you specify a high-level prompt to allow Copilot at a high level of autonomy to plan changes in steps, select files, and run tools or terminal commands, iterating on code edits until it is complete.

Since we want to ask questions regarding our codebase, let's set the mode to `Ask`.

The next dropdown is the AI language model being used.
By default, this is set to `Auto` so that Copilot will decide the model.
However, for consistency in this training, let's select the entry for `Claude Haiki 4.5`.

Let's now ask the very high level question: `What does this code do?`, and press enter.
You'll likely be asked whether you want to enable Claude Haiku 4.5 for all clients - select `Enable` when prompted.

You'll find the response looks something like the following:

```
This code generates visualization plots for inflammation data:

1. Loads data files: Uses glob to find all CSV files matching the pattern inflammation-*.csv in the ../data/ directory, sorts them, and limits processing to the first 3 files.

2. Processes each file: For each CSV file, it:
   - Loads the data as a NumPy array using comma delimiters
   - Creates a figure with 3 subplots arranged horizontally

3. Generates three plots showing statistical summaries across patients (rows):
   - Left plot: Average inflammation values per day
   - Middle plot: Maximum inflammation values per day
   - Right plot: Minimum inflammation values per day

4. Saves output: Each figure is saved as a PNG file with the same name as the input CSV file plus .png extension.
```

::::::::::::::::::::::::::::::::::::: callout

## Why Aren't I Seeing the Same Response?

You'll likely find it's not exactly the same.
Due to the ways in which LLMs process requests, based on an iterative probabilistic model,
responses based on the same question will show differences.
This effect is often visibly compounded over time, as the probabilistic outcome of a response generates an increasingly different result.

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## What do I Need to Know?

Ask the following questions about the code:

1. What are the main packages used?
2. How is Matplotlib used to generate the plots?

:::::::::::::::::::::::::: solution

1. Describe the main packages used? e.g.

```
1. glob: Built-in Python module for file pattern matching
   - glob.glob() finds all files matching a wildcard pattern (inflammation-*.csv)
   - Useful for batch processing multiple files with consistent naming

2. numpy: Numerical computing library
   - np.loadtxt() loads CSV data into a NumPy array
   - data.mean(axis=0), data.max(axis=0), data.min(axis=0) compute statistics across patients (rows) for each day (columns)

3. matplotlib.pyplot: Plotting library for creating visualizations
   - plt.figure() creates a new figure window
   - fig.add_subplot() adds subplots to the figure
   - axes.set_ylabel() and axes.plot() configure and draw the plots
   - fig.tight_layout() optimizes spacing
   - fig.savefig() exports the figure as an image file

These three packages work together: glob finds the files, numpy processes the data, and matplotlib visualizes the results.
```

2. How is Matplotlib used to generate the plots? e.g.

```
This script uses Matplotlib to create and save visualization plots:

1. Create a figure: plt.figure(figsize=(10.0, 3.0)) creates a new figure with dimensions 10 inches wide by 3 inches tall.

2. Add subplots: fig.add_subplot(1, 3, n) creates a grid of 1 row and 3 columns, with n specifying which subplot (1, 2, or 3):
   - axes1, axes2, axes3 are the three subplot axes objects

3. Label and plot data:
   - axes.set_ylabel() adds a label to the y-axis
   - axes.plot() draws a line plot of the data on that subplot
   - Each subplot shows a different calculation: mean(), max(), and min()

4. Layout adjustment: fig.tight_layout() automatically adjusts spacing between subplots to prevent overlap.

5. Save output: fig.savefig() saves the entire figure as a PNG image file.
```

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

FIXME: overlapping information, extract what's useful

::::::::::::::::::::::::::::::::::::: keypoints 

- FIXME

::::::::::::::::::::::::::::::::::::::::::::::::
