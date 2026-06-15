---
title: "Investigate a New Codebase"
teaching: 10
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can I use Copilot in a defined and repeatable way to explore new codebases?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Investigate a new codebase in terms of purpose and areas for improvement.
- Write and use a reusable prompt to understand a codebase.
- Write and use a reusable prompt to conduct a code review.

::::::::::::::::::::::::::::::::::::::::::::::::

In this episode we'll investigate a new codebase to increase our understanding of how it operates
and to identify strengths, weaknesses and ways to improve it.

## Preparing Useful Prompts

We've seen how we are able to reuse prompts by storing them in a prompt file.
Before we go ahead and investigate a new codebase,
let's add some reusable specialist prompts to help conduct this investigation for us.

### Prompt to Explain a Codebase

Let's start with a prompt to help us understand a codebase.
Here's an example code review prompt file based on one from the [GitHub Docs](https://docs.github.com/en/copilot/tutorials/customization-library/prompt-files/your-first-prompt-file#code-explanation-prompt).
Add the following draft to a new prompt file at `.github/prompts/explain-code.prompt.md`:

```markdown
---
description: 'Generate a clear code explanation with examples'
agent: 'agent'
---

Explain the following code in a clear, beginner-friendly way:

Please provide:

* A brief overview of what the code does
* A step-by-step breakdown of the main parts
* Explanation of any key concepts or terminology
* A simple example showing how it works
* Common use cases or when you might use this approach

Use clear, simple language and avoid unnecessary jargon.
```

:::::::::::::::::::::::::::::::::::::: challenge

## How Do You Understand a Codebase?

3 mins.

When investigating a new codebase, what is it that really helps you to understand what it does and how it works?
Tailor the `explain-code.prompt.md` file to include this criteria.

:::::::::::::::::::::::::: solution
:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

### Prompt to Conduct a Code Review

Next, let's add a reusable prompt to conduct a code review of a codebase,
to help us understand it's strengths and weaknesses,
and what needs to be fixed.

Here's an example code review prompt file based on one from the [GitHub Docs](https://docs.github.com/en/copilot/tutorials/customization-library/prompt-files/review-code).
Copy this into a `.github/prompts/review-code.prompt.md` file:

```markdown
---
description: 'Perform a comprehensive code review'
agent: 'agent'
---

## Role

You're a senior software engineer conducting a thorough code review. Provide constructive, actionable feedback.

## Review Areas

Analyze the selected code for:

1. **Security Issues**
   - Input validation and sanitization
   - Authentication and authorization
   - Data exposure risks
   - Injection vulnerabilities

2. **Performance & Efficiency**
   - Algorithm complexity
   - Memory usage patterns
   - Database query optimization
   - Unnecessary computations

3. **Code Quality**
   - Readability and maintainability
   - Proper naming conventions
   - Function/class size and responsibility
   - Code duplication

4. **Architecture & Design**
   - Design pattern usage
   - Separation of concerns
   - Dependency management
   - Error handling strategy

5. **Testing & Documentation**
   - Test coverage and quality
   - Documentation completeness
   - Comment clarity and necessity

## Output Format

Provide feedback as:

**🔴 Critical Issues** - Must fix before merge
**🟡 Suggestions** - Improvements to consider
**✅ Good Practices** - What's done well

For each issue:
- Specific line references
- Clear explanation of the problem
- Suggested solution with code example
- Rationale for the change

Be constructive and educational in your feedback.
```

:::::::::::::::::::::::::::::::::::::: challenge

## How Do You do a Code Review?

3 mins.

If you were to conduct a code review of a codebase,
how would you go about it?
Which areas would you look at and how would you investigate them?
Tailor the `review-code.prompt.md` file to include this criteria.

:::::::::::::::::::::::::: solution
:::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## Investigate!

20 mins.

Pick a GitHub code repository of your choice.
It could be something you (or your group) has written, something you're planning on using,
or something you're simply interested in.

Clone the repository to your local machine,
and use the prompts you've just created to build an understanding of the codebase and explore it's strengths and weaknesses.

Do you agree with the assessments?
Are they useful?
How could you improve them for use in the future?

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints 

- Build an array of useful reusable prompts to accomplish specific tasks related to software development.
- Review their usefulness and improve them over time.

::::::::::::::::::::::::::::::::::::::::::::::::
