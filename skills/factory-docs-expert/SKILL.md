---
name: factory-docs-expert
description: Search and read Factory AI documentation from docs.factory.ai/guides. Use when request related to Factory/Droid configuration, skills, hooks, droids, AGENTS.md, memory, rules, slash command etc.
---

# Factory Docs Expert

## When to Use
Invoke this skill when the user asks about:
- Factory AI capabilities, configuration, or best practices
- Skills, hooks, custom droids, or AGENTS.md setup
- Memory management, context, or token optimization
- Prompt crafting for different models
- Rules and conventions for teams
- Any workflow covered in docs.factory.ai/guides

## Instructions

### Step 1: Discover Available Guides
Fetch `https://docs.factory.ai/guides` to get the list of available guides and their sections.

### Step 2: Identify Relevant Links
Parse the page to find links that match the user's request. Each link is a requirement-link pair:
- The link text/anchor describes what topic it covers
- The URL points to detailed documentation

### Step 3: Fetch Relevant Documentation
For each matching guide section, fetch the full documentation page using FetchUrl.

### Step 4: Extract and Present Actionable Guidance
Provide:
- Summary of the relevant documentation
- Key steps or instructions from the docs
- Links to specific sections for reference
- Any code examples or configurations mentioned

## Common Request Patterns

| User Request | Relevant Guides |
|-------------|-----------------|
| "How do I create a skill?" | Skills > Quickstart, Skills > Cookbook |
| "Set up memory persistence" | Power User > Memory Management |
| "Configure hooks" | CLI Configuration > Hooks Guide |
| "Write AGENTS.md" | CLI Configuration > AGENTS.md |
| "Optimize token usage" | Power User > Token Efficiency |
| "Prompt crafting for Claude" | Power User > Prompt Crafting |
| "Set up team conventions" | Power User > Rules & Conventions |

## Best Practices
- Always fetch the actual docs rather than relying on memory
- Provide specific links and section references
- Include code examples when available in the docs
- Suggest related guides that might be helpful
- Never fabricate documentation - fetch and verify

## Output Format
Present findings as:
1. **Summary** - What the documentation covers
2. **Key Steps** - Numbered steps from the guide
3. **Code Examples** - Any configuration snippets
4. **Next Steps** - Related guides to explore
5. **Direct Links** - URLs for reference
