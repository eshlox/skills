# Documentation style guide

How to write and review documentation in this repository so developers find the
right answer fast.

Core goal: documentation that is short, complete, easy to scan, easy to search,
and easy to understand for non-native English speakers.

## When to use this guide

Apply it to every reader-facing page:

- The public documentation site, if the project has one.
- Package and app READMEs.
- Contributor docs (`docs/contributing/`).

Do not rewrite Architecture Decision Records (`docs/architecture/decisions/`).
They are dated historical records. Add a new ADR instead of editing an old one.

## Principles

1. One page, one main reader goal.
2. Put the answer first.
3. Use plain English and short sentences.
4. Use short paragraphs and descriptive headings.
5. Prefer concrete examples over abstract explanation.
6. No marketing language.
7. No em dashes. No idioms, slang, or culture-specific references.
8. Do not say "easy", "simple", "quick", or "just" unless it is objectively true.
9. Define product-specific terms the first time you use them.
10. Link only when the link helps the reader finish the task. Use descriptive
    link text, never "click here".
11. Remove anything that does not help the reader understand, decide, build,
    debug, or verify.

## Page types

Classify every page as one type and write it to that type.

| Type            | Goal                                                          |
| --------------- | ------------------------------------------------------------- |
| Quickstart      | Reach a useful result fast.                                   |
| Tutorial        | Teach by walking through a realistic example.                 |
| How-to guide    | Complete one task.                                            |
| Reference       | Give exact facts: options, parameters, types, errors, limits. |
| Explanation     | Explain why something exists and when to use it.              |
| Troubleshooting | Diagnose and fix known problems.                              |

## Page structure

- Start with a title that matches the reader's goal.
- Add a one or two sentence summary.
- Put prerequisites before steps.
- Put the most common path before edge cases.
- Move advanced detail lower, or into a reference page.
- Use numbered steps for procedures. Use bullets only for short lists.
- Use tables for parameters, options, limits, and comparisons.
- Use sentence case for headings. Prefer action headings for tasks, for example
  "Create an API key" instead of "API key creation".
- Add a "Verify" section when the reader needs to confirm the task worked.
- Add a "Troubleshoot" section when common errors exist.
- Add "Next steps" only when there is a useful next action.

## Examples

Every important workflow needs at least one useful example. Each example should
have a goal, the code or command, the expected result, and a short explanation.
Add a common variation or a common error case when it helps.

Code examples:

- Make them copy-paste ready: include imports, setup, and required values.
- Use realistic names and values.
- Do not hide important logic. Do not use clever code.
- Do not include insecure, deprecated, or production-dangerous patterns.
- Say so clearly when an example is incomplete or not production-ready.
- Show expected output when it helps.

## Reference pages

- Be exact. Use tables.
- Include types, defaults, allowed values, limits, and examples.
- Do not mix long explanation into reference pages. Link to how-to guides for
  workflows.
- For APIs, document purpose, method and path, authentication, parameters,
  request body, response body, status codes, error codes, and a minimal example.
- For CLI commands, document purpose, syntax, arguments, flags, defaults,
  examples, and common errors.

## Style rules

- Use active voice and address the reader as "you".
- Prefer common words. Explain required jargon. Avoid non-standard abbreviations.
- Do not repeat the same idea in different words.
- Do not over-explain obvious steps. Do not under-explain surprising behavior.
- Add likely search terms naturally. Put key nouns and verbs near the start of
  headings so readers can scan and search.

## Product terms and contract

Keep the project's public terms consistent across all pages. They are part of
the public contract, so define them once and use them the same way everywhere.

Maintain a short list here of the terms, package names, entry points, public
events, and error types that this project exposes, or link to the authoritative
naming reference. Replace this paragraph with that list when the project has a
public contract to protect.

## Review checklist

Before you finalize a page, confirm it answers:

- What is this?
- When should I use it, and when should I not?
- What do I need before I start?
- How do I do it?
- How do I know it worked?
- What can go wrong?
- Where do I go next?

Then confirm:

- The page is as short as possible without losing required information.
- A busy developer can scan it and a non-native English speaker can read it.
- Examples are useful and realistic. Links and headings are clear.
- Nothing is duplicated or missing.
- There are no em dashes.

## Handling missing information

Do not invent facts. Make the safest assumption, mark it clearly, and list open
questions at the end of your change so a reviewer can resolve them.
