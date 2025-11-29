---
description: Record learnings from this session to docs/tips/
---

<task>
Review the conversation history and document valuable learnings in the docs/tips/ folder.
</task>

<quality_threshold>
Evaluate the learning value on a 100-point scale for TALL Stack (Laravel + Livewire + Alpine.js + Tailwind CSS + daisyUI) development.

**If the score is 50 or below, DO NOT create a file. Instead, explain why it doesn't meet the threshold.**
</quality_threshold>

<scoring_criteria>
<do_not_record score="≤50">
  <category name="trivial">Simple typo fixes, variable renames only</category>
  <category name="common_knowledge">Basic Laravel routing, general PHP syntax, standard best practices</category>
  <category name="user_error">Issues caused by unclear or incorrect user prompts</category>
  <category name="environment_specific">Problems unique to a specific development environment</category>
</do_not_record>

<should_record score="≥51">
  <category name="integration_pitfalls">TALL Stack integration issues (e.g., Livewire/Alpine.js scope conflicts)</category>
  <category name="framework_specifics">daisyUI-specific behaviors (CSS precedence, Flexbox interactions)</category>
  <category name="undocumented_behaviors">Unexpected framework interactions not in official docs</category>
  <category name="complex_debugging">Issues where error messages didn't clearly indicate root cause</category>
  <category name="llm_knowledge_gap">Information likely unknown to general LLMs (new version issues, multi-framework edge cases)</category>
</should_record>

<evaluation_questions>
1. Will other developers likely encounter this issue?
2. Is this information easily found in documentation or basic searches?
3. Does it contain TALL Stack-specific technical insights?
4. Will this significantly reduce future debugging time?
</evaluation_questions>
</scoring_criteria>

<content_to_extract>
<element name="problem">What went wrong (error messages, unexpected behaviors)</element>
<element name="cause">Why it occurred (technical reasons, configuration issues)</element>
<element name="solution">How it was fixed (specific code/config changes)</element>
<element name="best_practices">Knowledge to prevent similar issues in the future</element>
</content_to_extract>

<output_format language="ja">
**IMPORTANT: The output file must be written in Japanese markdown format.**

<template>
```markdown
# [Problem Title in Japanese]

## 問題

[Problem description and error messages in Japanese]

## 原因

[Root cause explanation in Japanese]

## 解決策

[Solution and code examples in Japanese]

## ベストプラクティス

[Future insights in Japanese]

## 関連する技術要素

[Technology stack used in Japanese]
```
</template>

<filename_rules>
- Use kebab-case (e.g., `alpine-js-scope-issues.md`)
- Clear, descriptive name
- Must not conflict with existing files
</filename_rules>
</output_format>

<execution_steps>
1. Extract valuable learnings from conversation history
2. Evaluate learning value (0-100 points)
3. If ≤50 points: Explain why and stop
4. If ≥51 points: Create markdown file in specified format (in Japanese)
5. Save to `docs/tips/[appropriate-filename].md`
6. Report saved file path
</execution_steps>

<reference_examples>
Review existing files in docs/tips/ for formatting consistency:
- alpine-js-scope-issues.md
- text-wrapping-in-daisyui.md
- livewire-file-upload-troubleshooting.md
</reference_examples>
