---
description: Make an agent reference document for a framework, SDK or API
argument-hint: "{framework} [languages] [output directory]"
---

# AI Doc: Framework Reference Generator

Make a reference document for one framework, SDK or API. Coding agents read this document before they write code with that framework. This prompt works with all coding agents and all projects.

## Request

$ARGUMENTS

## Instructions

### Step 1: Get the input

1. Read the `Request` section.
2. If the `Request` section is empty, or contains only the text `$ARGUMENTS`, use the message of the user as the request.
3. Find these values in the request:
   - **Framework:** the name of the framework, SDK or API. This value is necessary.
   - **Languages:** the programming languages for the examples. This value is optional.
   - **Output directory:** the directory for the document. This value is optional.
4. If the framework name is missing, ask the user for it. Use a question tool if you have one. If you do not, ask in plain text and wait for the answer.
5. If you cannot ask the user, stop. Report that the framework name is necessary.
6. If the user does not give a language, use the languages of the official SDKs.
7. Make the `{slug}` from the framework name. Use lowercase and snake_case. Examples: `e2b`, `fastapi`, `langgraph`.

### Step 2: Find the output location

1. If the user gives an output directory, use it.
2. If the user does not give one, look in the project root for a directory of agent reference documents. Examples: `ai_docs/`, `docs/ai/`, `.agents/docs/`.
3. If you find no such directory, use `ai_docs/` in the project root. Make the directory if it does not exist.
4. If you cannot write files, write the full document in your answer.
5. The output file is `{output directory}/{slug}.md`.

### Step 3: Examine the existing documents

1. List the files in the output directory.
2. If `{slug}.md` exists, read it. Update that file. Do not make a second file for the same framework.
3. If other reference documents exist, read one of them. Use the same heading style and tone, but keep the `Document Format` of this prompt.

### Step 4: Do the research

1. Use primary sources only. These are:
   - The official documentation and API reference.
   - The official SDK repository: README, examples, type definitions and changelog.
   - Official templates and cookbooks.
2. Use the web or documentation tools that you have.
3. If you have no web access, use only the sources that the user gives. You can also use the installed package source code. Tell the user about this limit in the report.
4. Record the current stable version of each package. Record the date of today.
5. Do not invent a function, a parameter, a default value or a limit.
6. If no primary source confirms an item, mark the item **[VERIFY]**. Write what is not clear and where to examine it.
7. If two sources do not agree, mark the item **[VERIFY]**. Write the two values.

### Step 5: Write the document

1. Use the `Document Format`. Keep the sections in the same order.
2. Replace each `{placeholder}` with real content.
3. If the framework does not have the feature of a section, remove the section and its heading.
4. Obey all the `Writing Rules`.

### Step 6: Do a check of the document

1. Examine the document against the `Validation Checklist`.
2. Correct each item that fails.
3. If the output directory has an index file (for example `README.md` or `index.md`), add or update one row for the document.

## Writing Rules

### Language: Simplified Technical English (ASD-STE100)

- Write one instruction in each sentence.
- Use 20 words or fewer for an instruction. Use 25 words or fewer for a description.
- Use the active voice. Use the imperative for instructions.
- Use one word for one concept. Do not use synonyms. Example: if you write "sandbox", do not also write "VM" or "environment" for the same thing.
- Use "must" for a requirement. Do not use "should" for a requirement.
- Do not use marketing words. Examples: "perfect", "easy", "blazing fast", "seamless".
- Put numbers and units in facts. Example: "Starts in approximately 150 ms", not "starts quickly".

### Code

- Each code block must run without changes when the environment variables are set.
- Include all imports in each code block.
- Do not use variables or functions that the code block does not define.
- Put each language in its own code block, under its own heading. Do not put two languages in one code block.
- Put default values, units and limits in a comment on the related line. Example: `timeout=300  # seconds; default 300`.
- Release resources in each example. Use a context manager, `try`/`finally`, or an explicit close call.
- Show error handling in examples that can fail.

### Neutrality

- Write only facts about the framework. Do not write about a specific project that uses the framework.
- Do not write a "which API do I use?" section.
- Do not write instructions for one specific AI agent or AI tool.
- If an example calls an AI model, do not write a model name in the code. Read the model name from an environment variable. Example: `model=os.environ["MODEL_NAME"]`.
- Do not write prices. Prices change frequently. Write a link to the pricing page.

### Common defects that you must not make

- No version and no date. Always write the `Version` line.
- Hard-coded AI model names. Use an environment variable.
- Undefined variables in examples. Define all variables.
- Two languages in one code block. Use one block for each language.
- Prices in the document. Use a link.
- Website text: navigation menus, "Copy" buttons, anchor links and sales sentences. Remove it.

## Document Format

````markdown
# {Framework} - Agent Reference

{One sentence: what the framework is and what it does.}

> **Version:** {package}@{version} ({language}), {package}@{version} ({language}). **Date:** {YYYY-MM-DD}.
> **Sources:** {primary source URLs}.
> Items marked **[VERIFY]** are not confirmed by a primary source.

## Overview

{Two to four sentences: what the framework does, how it works, and the main object.}

### Key Features

- **{Feature}:** {fact with a number or unit}

## Quick Start ({Language})

### 1. Install

```bash
{install command}
```

### 2. Set the Environment Variables

```bash
export {ENV_VAR}="{value}"   # Get it from {location}. Do not commit it.
```

### 3. Basic Usage

```{language}
{shortest complete program that makes the main object, does one operation and releases the object}
```

### 4. Complete Example

```{language}
{one complete program that uses two or three features together}
```

{Repeat "Quick Start" for each language.}

## {Main Object} Lifecycle

{Make, configure, get information, keep alive, pause and resume, and release the main object.}

### {Lifecycle Operation}

#### {Language}

```{language}
{code with defaults and limits in comments}
```

- {behavior: return value, side effect, persistence}

## Feature Reference

### {Feature Name}

{One sentence: what the feature does.}

#### {Language}

```{language}
{code}
```

- {behavior and limits}

{Repeat for each feature.}

## Configuration and Environment Variables

### Default Values

| Variable or Setting | Default   | Description   |
| ------------------- | --------- | ------------- |
| `{name}`            | `{value}` | {description} |

### Scopes

| Scope   | Where to Set It | Applies To |
| ------- | --------------- | ---------- |
| {scope} | {method}        | {target}   |

### Priority Order

1. {highest priority}
2. {next}
3. {lowest priority}

## Integrations

### {Library or Provider}

#### {Language}

```{language}
{complete program; model names and keys come from environment variables}
```

## Common Use Cases

### {Use Case}

#### {Language}

```{language}
{complete program}
```

{Write three to five use cases.}

## CLI Reference

| Command     | Purpose   |
| ----------- | --------- |
| `{command}` | {purpose} |

## Best Practices

### Resource Management

{code and rules}

### Error Handling

{code with the real error types and fields}

### Long-Running Operations

{code and rules}

### Security

- {rule for secrets, untrusted input and permissions}

## Limits and Quotas

| Limit   | Value   | Notes   |
| ------- | ------- | ------- |
| {limit} | {value} | {notes} |

Prices: {link to the pricing page}.

## Troubleshooting

| Symptom   | Cause   | Correction   |
| --------- | ------- | ------------ |
| {symptom} | {cause} | {correction} |

### Debug Commands

```{language}
{code that shows versions, resources, network and configuration}
```

## Resources

- Documentation: {url}
- API reference: {url}
- SDK repository: {url}
- Examples: {url}
- Changelog: {url}
````

## Validation Checklist

- [ ] The `Version` line has the package versions, the date and the source URLs.
- [ ] Each code block has its imports and runs without changes.
- [ ] No code block uses an undefined variable or function.
- [ ] No code block has two languages.
- [ ] No code block has a hard-coded AI model name.
- [ ] Each function, default value and limit has a primary source, or has a **[VERIFY]** mark.
- [ ] Each example releases its resources.
- [ ] The document has no project-specific content and no "which API do I use?" section.
- [ ] The document has no prices, marketing words or website navigation text.
- [ ] Each sentence obeys the Simplified Technical English rules.
- [ ] If the output directory has an index file, the index has a row for the document.

## Report

- Write the path of the document. Write the package versions and the date.
- List the sections and the use cases in the document.
- List each **[VERIFY]** item.
- If you had no web access, say which sources you used.
