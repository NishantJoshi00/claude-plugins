---
description: Create user personas to test and vet your work
---

# Critic Command

## Arguments

The user provided: $ARGUMENTS

**Expected format:** `<count> <profile and situation>, <what to vet>`

Example: `5 skeptical developers scrolling twitter, vetting this launch post`

**Parse the arguments to extract:**
1. **Count** - Number of personas (e.g., "5", "3")
2. **Profile and situation** - User type and context (e.g., "skeptical developers scrolling twitter", "busy founders visiting a landing page")
3. **What to vet** - The content, flow, or artifact to review (e.g., "this launch post", "the signup flow", "README.md")

**If any of these are unclear or missing, ask the user before proceeding.**

**After parsing, clarify how to access the content:**
- If "what to vet" references "this", "the above", or is ambiguous, ask the user to paste the content or provide a file path
- If it's a file path (e.g., "README.md", "docs/landing.html"), confirm the path exists
- If it's a workflow or flow (e.g., "signup flow"), ask what you should review (code, UI, user journey)

**You should ask questions when needed** - don't guess or assume. Get clarity before launching personas.

---

## Execution

**CRITICAL: You MUST launch all personas in parallel.**

Create the specified number of personas using the **Task tool with subagent_type=general-purpose**.

To run them in parallel, you MUST:
- Make multiple Task tool calls in a **single message**
- Do NOT wait for one persona to finish before starting the next
- Launch all N personas at once

Each persona task should:
- Be given a unique name, background, and mindset
- Be provided with clear access to the content (file path, pasted text, or specific instructions)
- Review the specified content/flow from their perspective
- Act realistically (see Persona Behavior below)

**Before launching personas, ensure you have:**
- Confirmed what content to review
- Have access to that content (file, conversation context, or user-provided text)
- Clarified any ambiguities with the user

---

## Persona Behavior

Each persona must act like a real user in the given situation:
- They can get confused
- They can lose interest and drop off
- They can misunderstand things
- They can stumble on unclear copy or broken flows
- They can get distracted
- They can miss things entirely

Simulate realistic user behavior for the situation. Not every user completes the journey.

---

## Output Format

After all personas complete, aggregate their findings.

For each persona, report:
1. **Name, background, and mindset** entering the situation
2. **Their experience** step by step
3. **Where they stumbled, disengaged, or succeeded**
4. **Actionable issues** from their perspective

**End with aggregated recommendations** across all personas, highlighting common patterns and critical issues.

---

## Example Usage

```
/critic 5 skeptical developers scrolling twitter, vetting this launch post for SkillSync
```

This would create 5 developer personas who critically review a Twitter launch post.
