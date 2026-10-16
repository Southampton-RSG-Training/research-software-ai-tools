---
title: "How to use Copilot to Improve an Existing Codebase"
teaching: 30
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can Copilot help me improve my code?
- What can I do to improve my Copilot prompts?
- How can I create and use reusable Copilot skills?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Describe how to use prompt engineering to obtain valuable responses from Copilot
- Use Copilot to improve a segment of code
- Use Copilot to add a new, small feature to an existing codebase
- Describe how to use Copilot to assist with Git commit messages
- Create and use a reusable Copilot skill

::::::::::::::::::::::::::::::::::::::::::::::::

In the previous episode we looked at Copilot giving us guidance and advice to improve our code.
In this episode, we'll look at how Copilot can assist with code modifications more directly,
looking at the following features:

- `Inline suggestions` - where Copilot provides coding suggestions as you type
- `Agent mode` - where Copilot directly autonomously undertakes either small or large scale changes on request, with a single option to approve the changes at the end of the process

These are in ascending order of autonomy, authority and scope that we delegate to Copilot to make changes.
As we'll see, as we delegate more authority and scope,
the more we should increase our skepticism and diligence in reviewing and understanding suggestions made by such tools.

## Inline Suggestions

Within VSCode, Copilot can provide "inline" suggestions as we type,
which go much further than typical IDE autocomplete suggestions.

If we select the Copilot icon again in the status bar,
we can see the current inline settings:

![](fig/copilot-inline-settings.png)

So here, we can see that inline settings are:

- Enabled for `Ghost text suggestions`, where suggestions appear as faded text
- Partially enabled for `Ghost text suggestions for Instructions`, since we have an instructions file for this project
- Enabled for `Next edit suggestions`, where it may predict changes that go beyond the immediate context to make suggestions in other places in your code
- An `Eagerness` setting, so if you find inline suggestions appear too quickly and disrupt your flow, or aren't appearing fast enough, you can set this here

These suggestions will appear as "ghosted text" suggestion which you can autocomplete with tab,
very similar to how they appear with standard VSCode autocomplete.

Let's say we want to add a new section describing our coding style.
Add the following at the bottom of the `Coding style and formatting section`:

```markdown
- In docstrings
```

You should see a suggestion appear direcly after your cursor,
something like `include a description of the function's purpose, its parameters, and its return value`.
You can accept this suggestion by pressing `Tab`.
If you continue to add new lines after this, you may find it continues to suggest other things to include,
such as:

```markdown
### Coding Style
...

- Use descriptive variable names that convey the purpose of the variable
- Use single quotes for strings unless the string contains a single quote, in which case use double quotes
```

It does this by rapidly incorporating contextual information from a number of sources to infer a suggestion,
including:

- The code file you are editing
- Any code you have currently selected
- Frameworks, languages and dependencies
- Any instructions file

Copilot suggestions are a starting point, but we should always review, understand, and amend as necessary,
as opposed to blindly accepting suggestions.

:::::::::::::::::::::::::::::::::::::: challenge

## Amend the Suggestions

5 mins.

Review and then amend the `Code style and formatting` section as you see fit, perhaps to fit your coding style.

:::::::::::::::::::::::::: solution

For example:

```markdown
- Follow PEP 8 style guide
- Maintain 4 spaces for each level of indentation
- Add function and class docstrings in the reStructuredText format
- In docstrings, include a description of the function's purpose, its parameters, and its return value
- Use descriptive variable names that convey the purpose of the variable
- Use single quotes for strings unless the string contains a single quote, in which case use double quotes
```

As we'll see shortly, these coding style guidelines will inform future refactoring of our code.

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## Inline Suggestions for Code

5 mins.

In `inflammation-plot.py`, begin adding an additional parameter to the functions calls in the code,
by placing an additional `, ` at the end of the given list of parameters, and see which inline suggestions are being made, e.g.:

```python
    data = np.loadtxt(fname=filename, delimiter=',', ... )
```

Try this for the following function calls:
- `np.loadtxt`
- `plt.figure`
- Each of the `.plot` calls to the `axes` variables

1. What's being suggested?
1. Are the suggestions helpful? Are they always the same?
1. Does the code run as you expect?

:::::::::::::::::::::::::: solution

1. For example:

```python
    data = np.loadtxt(fname=filename, delimiter=',', dtype=np.float32)
```

The inline suggestion for `plt.figure` suggested `constrained_layout=100`,
which wasn't approved since it doesn't add any feature we want.

For `.plot`, if the first suggestion of a `color` parameter is selected,
it suggests variants of that for the other calls to `plot`, e.g.

```python
    axes1.plot(data.mean(axis=0), color='blue')
    axes2.plot(data.mean(axis=0), color='red')
    axes3.plot(data.mean(axis=0), color='green')
```

:::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::: solution
:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

## Agent Mode: Small Changes

Agent mode differs from inline suggestions by offering the ability to enact changes step-by-step directly on your approval.
Unlike inline suggestions which appear as you type, this mode allows you to request broader changes across multiple lines or functions,
so it's ideal for repetive things like small-scale refactoring of code logic or renaming variables.
It represents a middle ground in terms of autonomy — more direct than inline suggestions but less autonomous than Plan mode.

To get started with using Copilot to make a small edit, you highlight the code you want to modify before requesting the change you want.

For example:

1. Select `+` to create a new chat conversation
1. Select `Local` harness
1. Select `inflammation-plot.py` in the chat context
1. Select the entire for loop in `inflammation-plot.py`; you'll notice that the context now includes this file with the selected line numbers
1. Enter `Add a comment about this code above this loop` into the chat
1. Press `Enter`

You'll now see a comment added above the loop highlighted in green, e.g.

```python
# Plot the average, maximum, and minimum inflammation for each dataset.
```

You’ll also see a `Keep` and `Undo` pop-up options displayed next to the suggestion.
Read through the comment, and if you agree that the comment summarises the code sufficiently, select `Keep`.

::::::::::::::::::::::::::::::::: callout

## The Temptation to Blindly Accept!

So note that here, we properly scrutinise the suggestion as opposed to accepting it blindly!
it would be all too easy to just assume it's correct and just accept it,
but it's helpful to remember that tools like Copilot are like a more helpful autocomplete,
not a thinking teammate.
As such, skepticism and review must become a key practice when using such tools.

:::::::::::::::::::::::::::::::::::::::::

### Copilot and Commit Messages

What's also useful is that we can have Copilot draft Git commit messages for us too.
Sometimes writing concise messages is a bit of a pain, and this can help shortcut this activity a bit.
It's also useful as an indicator of the scope of what we've changed semantically,
although since Copilot aims to be concise, it may miss some key details.

Let's add the changes we've made so far to the Git staging area:

1. Select `Source Control` in the navigation bar (the third one down)
1. Select the `+` icon next to `inflammation-plot.py` in the `Changes` list, which will add our changes so far to the Git staging area
1. Select the sparkle icon next to the `Message` text box

You should see something like:

`Enhance inflammation plot script with data type specification and color coding for plots`

Of course, we should vet and edit (or ask Copilot to retry) this description accordingly.
In this case, it doesn't mention about the DPI setting which might be a particular nuance we wish to add,
so again, we need to review what Copilot suggests.

Also worth noting is that if we wanted to reference a repository issue number in our commit message,
we should remember to add that as well.

Once we're happy with it, we can then select `Commit` to commit our changes to our local repository.

:::::::::::::::::::::::::::::::::::::: challenge

## A Small Refactor!

5 mins.

Let's assume we want to rename the `axes` variables to have the prefix `subplot` instead,
e.g. instead of `axes1`, we'd have `subplot1`.

Using the `Local` harness, have Copilot agent mode rename all of these variables by selecting the appropriate code in the editor and entering the request in the chat window,
then verify and accept the changes if you agree with them.
Does the code still run correctly?

Note: after selecting the code you want to change,
you can also request edits by typing `Ctrl` + `I` (Linux) or `Cmd Key/Windows Key` + `I` (Mac/Windows) to have a small pop-up appear to type in your request,
which is quicker and sometimes more convenient if it's a small request.

:::::::::::::::::::::::::: solution

1. Select the code from the first `axes1` definition to the last use of `subplot3`, e.g.

   ```python
       axes1 = fig.add_subplot(1, 3, 1)
       axes2 = fig.add_subplot(1, 3, 2)
       axes3 = fig.add_subplot(1, 3, 3)

       axes1.set_ylabel('average')
       axes1.plot(data.mean(axis=0))

       axes2.set_ylabel('max')
       axes2.plot(data.max(axis=0))

       axes3.set_ylabel('min')
       axes3.plot(data.min(axis=0))
   ```

1. Enter `Rename axes variables to have a subplot prefix instead` into the chat
1. Press `Enter` and you should see something like the following, where VSCode is giving you the option of `Keep`ing or `Undo`ing each of the changes:
   ![](fig/copilot-rename-variables.png)
1. After reviewing each of the suggestions, select `Keep`
1. Verify that the code still runs correctly.

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::


## Agent Mode: Larger-scale Changes

We can also ask Copilot in agent mode to make much larger, potentially multi-file changes across our codebase.
So instead of asking Copilot to change a specific piece of code, you give it a goal, such as adding a feature, or refactoring a module.
Copilot then plans how to achieve that goal and works across the repository to do so.
It may read and modify multiple files, add or update tests, adjust configuration, and iterate over several steps before presenting the result.
In this way, agent mode behaves more like a junior developer taking on a task, rather than a pair programmer responding line-by-line.

Note the increase in authority to modify code, which represents a much greater risk:
the impact of changes is greater and requires more careful (and potentially more involved) review.

In the last episode we looked at the suggestions made by two Copilot models to improve the code.
Let's now use agent mode to do this as a refactoring activity,
directly amending our code with the goal to improve its readability.

1. Select `+` to create a new chat conversation
1. Select `Local` as the harness
1. Select `inflammation-plot.py` in the chat context
1. Enter the following prompt: `Refactor this code to improve its modularity and readability`
1. Press `Enter`
1. You may need to authorise various commands it wants to run as part of its codebase analysis and verification
1. Once suggested improvements appear, review the changes and either:
   - If you agree with them and think they are an improvement on the original code, `Keep` the suggestions
   - If you don't agree with them, cancel the suggestions and select the circular `Retry` icon at the bottom left of the chat response until you get something more acceptable

One example of output:

```python
"""
Analyze and visualize inflammation data.

This script reads inflammation CSV files from data/, computes statistics
(mean, max, min) across patients for each day, and saves corresponding
plots as PNG files.
"""

import glob
from pathlib import Path

import numpy as np
from matplotlib import pyplot as plt


def load_inflammation_data(filename: str) -> np.ndarray:
    """Load inflammation data from a CSV file.
    
    Args:
        filename: Path to the CSV file containing inflammation data.
        
    Returns:
        A 2D numpy array where rows are patients and columns are days.
    """
    return np.loadtxt(fname=filename, delimiter=',')


def create_statistics_plot(data: np.ndarray) -> plt.Figure:
    """Create a figure with three subplots showing mean, max, and min values.
    
    Args:
        data: A 2D numpy array of inflammation values.
        figure_size: Tuple of (width, height) for the figure in inches.
        
    Returns:
        The matplotlib Figure object containing the three subplots.
    """
    # Create subplots for mean, max, and min statistics
    fig, axes = plt.subplots(1, 3, figsize=(10.0, 3.0), constrained_layout=True)
    summaries = (
        ('average', 'blue', data.mean(axis=0)),
        ('max', 'red', data.max(axis=0)),
        ('min', 'green', data.min(axis=0)),
    )

    for axis, (label, color, values) in zip(axes, summaries):
        axis.set_ylabel(label)
        axis.plot(values, color=color)

    return fig


def process_inflammation_file(filename: str) -> None:
    """Load inflammation data and save a statistics plot.
    
    Args:
        filename: Path to the CSV file to process.
    """
    print(filename)
    data = load_inflammation_data(filename)
    fig = create_statistics_plot(data)
    output_filename = f"{filename}.png"
    fig.savefig(output_filename)
    plt.close(fig)


def main() -> None:
    """Load and process all inflammation data files."""
    filenames = sorted(glob.glob('data/inflammation-*.csv'))
    for filename in filenames:
        process_inflammation_file(filename)


if __name__ == '__main__':
    main()
```

So in this instance, we can see that there are a whole swathe of changes:

- Modularised the codebase by refactoring into four functions: use of a main function called from the top-level script, for loading a CSV file, generating a plot for a set of data, and processing a particular inflammation file
- Docstrings have been added for each of the functions and the module
- The processing of the average, maximum and minimum values has been refactored into a loop iterating over a data structure
- The subplots are generated within a loop using `zip()` to provide corresponding pairs of array elements into the loop.
If we didn't like this particular style, we might use Edit mode on this segment to simplify it

Note that it differs substantially from the version shown from a similar question made in Ask mode earlier,
and whilst it is more modular,
it's now 127 lines of code where before it was 32 lines - 
we might consider this to be quite an over-engineered overkill.

It has also introduced additional complexity, using a loop and a `zip` function to set the labels and generate plots for each graph.
This is a common risk with using AI tools, where the level of complexity can grow quickly if we're not careful,
with the code becoming something we can't easily understand.
We have to measure accepting such suggestions with the increasing difficulty in maintaining the codebase.
Essentially: don't accept anything you don't understand!

::::::::::::::::::::::::::::::::: callout

## What if I don't get a Good Response?

If you aren't getting a good response despite retrying several times,
it suggests that the prompt is either not reflective of what you're really after or isn't specific enough,
so try amending the request.

:::::::::::::::::::::::::::::::::::::::::

Now once the suggestions have been integrated,
we're still able to undo these changes, e.g. either by selecting `Edit` and `Undo` from the VSCode menu,
or pressing `Ctrl + Z` (or `Cmd/Windows Key + Z`).
We're also able to edit a previous prompt in the chat window,
perhaps adding more specifics for what we want.

::::::::::::::::::::::::::::::::::::::::: instructor

## Checkpoint: Check that the code runs as expected

::::::::::::::::::::::::::::::::::::::::: 

:::::::::::::::::::::::::::::::::::::: challenge

## A Large Refactor!

3 mins.

Perhaps the suggestions look generally quite good,
but maybe it isn't quite what we're after.

Ensuring you have `Local` harness and the `inflammation-plot.py` script selected,
ask Copilot to make changes as you see fit to improve this codebase.

:::::::::::::::::::::::::: solution

e.g. deciding to remove the loop and use of `zip` in the `create_statistics_plot()` function for simplicity,
by selecting the `create_statistics_plot()` function and requesting
`Remove the loop, keep the label setting and plot generation flat`,
this code was reduced to the simpler:

```python
   # Create subplots for mean, max, and min statistics
    fig, axes = plt.subplots(1, 3, figsize=(10.0, 3.0), constrained_layout=True)
    axes[0].set_ylabel('average')
    axes[0].plot(data.mean(axis=0), color='blue')
    axes[1].set_ylabel('max')
    axes[1].plot(data.max(axis=0), color='red')
    axes[2].set_ylabel('min')
    axes[2].plot(data.min(axis=0), color='green')
```

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::: instructor

## Quick Check: Ask the Audience

Following the exercise, paste the following comment into the chat, and ask for thumbs up/down as a reaction to it,
and summarise the responses:

Were you able to achieve something that you regard as well written code that you understand and runs?

:::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## A "Clever" Refactor!

5 mins.

Let's assume that we want to expand this codebase further.
Perhaps we know that the inflammation data format will change in the future,
in ways that mean the NumPy library isn't the ideal processing library of choice,
and that the Pandas library (which is a more general purpose data analysis library) will be a much better fit for this work.

Using the `Local` harness and `Agent` mode,
ask Copilot to refactor your code to use Pandas instead of NumPy:

Part 1:

1. Install Pandas into your virtual environment, e.g. `python -m pip install pandas`
1. Construct and enter a suitable prompt
1. Review and accept the changes
1. What do you need to do to be able to re-run the code?
1. Does the code generate the correct results?
1. Add the changes to Git staging area, Ask Copilot to generate a commit message, amend as necessary, and commit the change

Part 2:

- If you already know Pandas, do the changes look sensible?
- If you don't know Pandas, what are the risks of accepting these changes?

:::::::::::::::::::::::::: solution

Part 1:

After installing Pandas into the virtual environment, e.g.

Prompt: `Modify this code to use Pandas instead of NumPy. Use the virtual environment that already exists`

```python
"""
Analyze and visualize inflammation data.

This script reads inflammation CSV files from data/, computes statistics
(mean, max, min) across patients for each day, and saves corresponding
plots as PNG files.
"""

import glob

import pandas as pd
from matplotlib import pyplot as plt


def load_inflammation_data(filename: str) -> pd.DataFrame:
    """Load inflammation data from a CSV file.
    
    Args:
        filename: Path to the CSV file containing inflammation data.
        
    Returns:
        A DataFrame where rows are patients and columns are days.
    """
    return pd.read_csv(filename, header=None)


def create_statistics_plot(data: pd.DataFrame) -> plt.Figure:
    """Create a figure with three subplots showing mean, max, and min values.
    
    Args:
        data: A DataFrame of inflammation values.
        
    Returns:
        The matplotlib Figure object containing the three subplots.
    """
    # Create subplots for mean, max, and min statistics
    fig, axes = plt.subplots(1, 3, figsize=(10.0, 3.0), constrained_layout=True)
    axes[0].set_ylabel('average')
    axes[0].plot(data.mean(axis=0), color='blue')
    axes[1].set_ylabel('max')
    axes[1].plot(data.max(axis=0), color='red')
    axes[2].set_ylabel('min')
    axes[2].plot(data.min(axis=0), color='green')

    return fig


def process_inflammation_file(filename: str) -> None:
    """Load inflammation data and save a statistics plot.
    
    Args:
        filename: Path to the CSV file to process.
    """
    print(filename)
    data = load_inflammation_data(filename)
    fig = create_statistics_plot(data)
    output_filename = f"{filename}.png"
    fig.savefig(output_filename)
    plt.close(fig)


def main() -> None:
    """Load and process all inflammation data files."""
    filenames = sorted(glob.glob('data/inflammation-*.csv'))
    for filename in filenames:
        process_inflammation_file(filename)


if __name__ == '__main__':
    main()
```

:::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::: solution

Part 2:

If you don't already know Pandas,
there is a considerable risk with this type of refactoring:
by accepting these modifications,
we're including code without understanding the concepts or operations of Pandas.
This greatly increases the risk that we generate incorrect code,
and should be avoided.

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::: challenge

## Another Plot Please

3 mins.

Use agent mode to add the generation of a fourth plot to the code,
for standard deviation,
test the code to ensure it works,
then add and commit the changes with a Copilot-generated (and reviewed) commit message.

:::::::::::::::::::::::::: solution

Prompt: `Add a fourth axes plot for standard deviation`

```python
    # Create one subplot for each per-day statistic.
    fig, axes = plt.subplots(1, 4, figsize=(13.0, 3.0), constrained_layout=True)
    axes[0].set_ylabel('average')
    axes[0].plot(data.mean(axis=0), color='blue')
    axes[1].set_ylabel('max')
    axes[1].plot(data.max(axis=0), color='red')
    axes[2].set_ylabel('min')
    axes[2].plot(data.min(axis=0), color='green')
    axes[3].set_ylabel('standard deviation')
    axes[3].plot(data.std(axis=0), color='orange')
```

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::: instructor

For the next exercise, in the shared notes document have a section for participants to add in answers.

:::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## Class Discussion: What Will *You* Change?

5 mins.

How do you see AI coding assistants like Copilot changing your working practices?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::: callout

## The Importance of Process

Process - the way we do things - is important in software engineering because it’s what leads towards reliable outcomes.
Without process we rely on tacit knowledge and luck.
But with process, we get repeatability, shared understanding, and the ability to improve over time.
Good process makes work visible, enforces quality at the right moments (design, review, testing, release),
and creates feedback loops so mistakes are caught early, when they’re cheapest to fix.
In science, reproducibility is a central tenet of research.
So as responsible researchers, we need to ensure we apply the same rigour to the software we write.

AI tools like Copilot make this more important, not less.
Whilst it accelerates code generation, it doesn't understand intent or consequences,
so a strong process ensures we use AI in an environment that amplifies good engineering habits instead of bypassing them.
The key principle is that process assigns responsibility to people, not tools.
Copilot speeds up execution, but process ensures accountability, quality, and sustainability.

:::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::: instructor

For the next exercise, in the shared notes document have a section for participants to add in answers.

:::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## Class Discussion: How Should we Mitigate The Risks of using AI Coding Tools?

5 mins.

What can we do to mitigate the risks of using AI coding tools like Copilot?
How should we adapt our day-to-day development to accommodate these changes,
not only for we use such tools with code, but also with our data?

:::::::::::::::::::::::::: solution

Some suggestions:

- Ensure suggested changes are throughly reviewed understood prior to their inclusion in the code
- Keep the context and scope of prompts (and their expression) to a minimum to accomplish a task,
to discourage large and/or complex suggestions that are difficult to understand
- In the case of refactored code, ensure suggested changes are throughly tested against the original version to ensure correct behaviour, i.e. manually, but also re-running a unit test suite if one exists and includes sufficient tests for the modified code
- Consider adding unit tests for AI-suggested changes or new features
- Ensure we continue to adhere to any project defined data management plan and institutional research data management policies

Note that many of these changes are accepted best practice for code written manually.
However since much less of our own cognition is involved in this style of development,
adopting a more critical and skeptical approach becomes even more important.

:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

## Reusable Code Skills

Skills in VSCode Copilot are reusable sets of instructions and supporting resources that teach Copilot how to complete a particular task.
They help you standardize work, save time, and ensure consistency when Copilot performs recurring tasks or follows specific project practices.

### How Reusable Skills Work

You can create a skill by placing its instructions in a `SKILL.md` file inside a skill-specific directory.
For example, a skill named `my-skill` resides at `.github/skills/my-skill/SKILL.md`.

Copilot can use a skill when its description matches the task at hand.
You can also invoke it explicitly in chat with `/` followed by the skill name
(e.g. `/my-skill`), then Copilot will follow the instructions using the current project context.

Skills help you:
- Reuse detailed task instructions and supporting resources
- Maintain consistency in how tasks are carried out
- Share workflows and best practices with your team

Common skills include workflows like generating a README, adding type annotations, or reviewing code.
We can adapt these to our specific project needs.

Let's create a reusable skill now.
Our code repository is currently lacking a README, so let's adapt a pre-existing skill.
There are many reusable and freely available Copilot resources at [Awesome GitHub Copilot](https://github.github.com/awesome-copilot/),
including agents, skills, and instruction files, all available from a GitHub repository.

Let's first obtain a reusable skill for generating README files.
Take a look at https://raw.githubusercontent.com/github/awesome-copilot/refs/heads/main/skills/readme-blueprint-generator/SKILL.md:

Looking at the file, we can see a number of structural features:

- A metadata header at the top, describing the skill and when it should be used
- A sequence of steps to follow, in this case starting with scanning a certain set of files to build context, using any `copilot-instructions.md` file, and generating a sections each based on specific criteria
- Some instructions clarifying how to format the README, and high-level guidance on how to write it

:::::::::::::::::::::::::: instructor

For the next exercise, add a section into the shared notes so that participants can add their own comments.

:::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## Create a Reusable Skill and Generate a README

10 mins.

1. Create a new skills directory at `.github/skills`
1. Create a new directory at `.github/skills/readme-blueprint-generator`
1. Download the [README generator skill](https://raw.githubusercontent.com/github/awesome-copilot/refs/heads/main/skills/readme-blueprint-generator/SKILL.md) into that directory as `SKILL.md`
1. Select agent mode and a model of your choice in the chat
1. Use the skill to generate a README by typing `/readme-blueprint-generator` into the chat. The chat will autocomplete the name. Press enter to invoke it
1. Select `Retry` if you want it to try again

Once generated, review, accept, and amend the README as you see fit.
You'll likely see things you want to correct or adapt!

Add a short description to the shared notes document describing what you think about what is generated:

- Generally, to what extent is the README is useful?
- What is incorrect and needs to be fixed?
- What is missing?

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints 

- Inline suggestions are made by Copilot as "ghosted text" in the editor which you autocomplete with the `Tab` key.
- Copilot can suggest small-scale modifications for your approval based on a segment of code by selecting the code and using `Edit` mode in the chat window (or pressing `Ctrl + I` or `Cmd/Windows Key + I`) and entering a request.
- Always review and never blindly accept AI-generated code suggestions.
- Copilot can write summary Git commit messages for us in VSCode by selecting the sparkle icon next to the commit message text box in the `Source control` navigation tab.
- Agent mode can suggest larger-scale modifications to our code across multiple files by using `Agent` mode in the chat window, and entering a more comprehensive and complex request.
- Select `Retry` to have Copilot re-generated a response.
- It's important to consider how to include AI-based coding assistants in your day-to-day development process to ensure accountability, quality, and sustainability are maintained within a codebase.
- Skills in VSCode Copilot are reusable instructions and resources that guide Copilot through specific tasks.

::::::::::::::::::::::::::::::::::::::::::::::::
