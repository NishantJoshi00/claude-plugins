---
description: Create user personas to test and vet your work
---

# Critic Command

## Arguments

The user provided: $ARGUMENTS

**This command accepts natural language input.** Examples:
- `what would senior engineers feel about this landing page`
- `5 skeptical developers scrolling twitter reviewing my launch post`
- `would busy founders sign up for this? simulate 3 personas`
- `junior devs looking at the README`

## Parsing Strategy

**Extract these elements from the natural language input:**

1. **Count** (default: 5 if not specified)
   - Look for explicit numbers: "5", "3", "seven"
   - Look for phrases: "simulate X personas", "X people"
   - Implied quantities: "a few" → 3, "several" → 5
   - If not found, use **default of 5**

2. **Persona** (required - ask if unclear)
   - Who: "senior engineers", "skeptical developers", "busy founders", "junior devs"
   - Optional context/situation: "scrolling twitter", "visiting a landing page", "looking at the README"
   - **If vague** ("people", "users", "someone") → **ASK** "Who specifically should I simulate?"
   - **If missing entirely** → **ASK** for persona description

3. **Target** (required - ask if unclear)
   - What to review: "this landing page", "my launch post", "the README", "signup flow"
   - Check if referenced content is:
     - In recent conversation ("this", "the above")
     - A file that exists in the project
     - Needs to be provided by user
   - **If ambiguous** ("this", "it") with no clear context → **ASK** what to review
   - **If missing entirely** → **ASK** what should be reviewed

## Confirmation Before Spawning

**CRITICAL: Always confirm before launching personas.**

After parsing, present to the user:
- **Count**: X personas
- **Who**: [persona description]
- **Reviewing**: [target description]
- **How you'll access it**: [file path / pasted content / conversation context]

Ask: "Should I proceed with spawning these personas?"

Only launch after user confirms.

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
