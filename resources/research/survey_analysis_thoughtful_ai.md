# Thoughtful AI for the Rubyist - Survey Analysis

## Survey Overview

**Total Responses:** 34 respondents across 3 surveys
- Survey 1 (Checked for AI Bias): 7 responses
- Survey 2 (Community): 10 responses
- Survey 3 (Main, internal company and external results): 17 responses

**Response Period:** September 22-27, 2025

---

## Key Statistics

### AI Tool Adoption Rates

**Current Usage Distribution:**
- **Regular users (Daily/Weekly)**: 35% (12/34)
- **Occasional users (Monthly)**: 18% (6/34)
- **Non-users by choice**: 32% (11/34)
- **Never used/Aware only**: 15% (5/34)

**Most Popular AI Tools:**
1. GitHub Copilot - 47% of users
2. Claude Code - 41% of users
3. ChatGPT - 41% of users
4. Cursor - 29% of users

### Ruby-Specific AI Performance Ratings (1-5 scale)

Based on aggregated responses where ratings were provided:

- **Blocks and iterators**: 3.4/5 (moderate success)
- **Rails conventions**: 3.2/5 (moderate success)
- **Ruby idioms/style**: 2.8/5 (below average)
- **Metaprogramming**: 1.8/5 (significant struggles)

### Primary Use Cases

**Top 5 AI Applications:**
1. Writing tests - 65% of AI users
2. Code generation/scaffolding - 59%
3. Debugging/explaining code - 59%
4. Refactoring existing code - 47%
5. Documentation - 35%

---

## Major Trends

### 1. Polarized Community Response
The Ruby community is deeply divided on AI adoption, with strong voices on both extremes:
- Enthusiastic daily users who see major productivity gains
- Staunch opponents citing ethical, environmental, and skill attrition concerns
- A cautious middle ground using AI selectively for specific tasks

### 2. "Use It or Lose It" Concern
Multiple respondents independently raised concerns about skill attrition:
- Fear of becoming dependent on expensive tools
- Worry about junior developers not learning fundamentals
- Concern that AI use reduces problem-solving abilities

### 3. Ruby-Specific Challenges
Consistent patterns in what AI struggles with:
- Modern Ruby syntax (endless methods, `it` blocks, omitting hash values)
- Rails "magic" and runtime symbol definitions
- Metaprogramming and DSLs
- Applying patterns from other languages (especially Python) to Ruby

### 4. Testing Paradox
While writing tests is the #1 use case, multiple respondents note:
- AI-generated tests are often "superficial" or "garbage"
- Tests require significant rework
- AI doesn't understand the intent behind tests

### 5. Context and Verification Essential
Successful users emphasize:
- Narrow, well-defined tasks work best
- Always verify and understand AI output
- Treat AI as a "rough draft" tool
- Never trust AI blindly

---

## Powerful Quotes (With Permission)

### On Dependency and Skill Attrition

> **"Don't bring a forklift to the gym. Human skills are 'use it or lose it.'"**
- Individual contributor, 11+ years experience

> **"Brain-task-based skills can be very 'use it or lose it'. The difference between using basic autocomplete and having an LLM generate entire blocks or even files, is _significant_."**
- Experienced developer on skill attrition

> **"My biggest concern is that dependency on LLM tooling creates an indentured class of developers, who are then at the whim of whatever premiums these companies decide to charge."**
- Developer comparing AI dependency to calculator use

### On Working with AI

> **"Let it rough draft, and you refine. If it doesn't get it right on the first or second try, don't get frustrated, just dip into the code and do it yourself."**
- Developer on practical AI usage

> **"Never assume the LLM is right, challenge everything they tell you."**
- Tech lead on verification

> **"Don't try to replace your brain with it, rather ask, how can I augment my abilities with it."**
- Developer on thoughtful integration

> **"Narrow the scope of the task and be specific - give the AI tool bite-sized, well-defined tasks with clear guardrails."**
- Developer on effective prompting

### On Ruby-Specific Issues

> **"It sometimes feels like the models are trying to apply code style or coding patterns from other programming languages or frameworks to Ruby."**
- Developer on language confusion

> **"Rails. It's magic for humans because symbols are defined at runtime and AI still has issues."**
- Developer on Rails challenges

> **"Any time you have mixed patterns in a codebase, you're likely to get the 'legacy' one copied at some point."**
- Developer on context window issues

### On Benefits When Used Well

> **"Having someone to talk to about my ideas and where I want to go. It helps me think things through and validate my ideas... It's like having a blog post custom made to my situation."**
- Developer on AI as thinking partner

> **"It helps me iterate on approaches rapidly so I can quickly identify if an approach will actually work."**
- Developer on rapid prototyping

> **"As a solo dev, it's a measure of last resort when stuck and there is nobody to ask."**
- Solo developer on AI as pair programmer substitute

### Critical Perspectives

> **"I also have grave concerns about nascent and novel devs, at the beginning of their journeys, becoming overly reliant on LLMs and not learning how to solve problems independently through research and synthesis."**
- Senior developer on learning impact

> **"It's fun, like going to a casino is fun. You're going to lose time/money, but you'll still want to play."**
- Developer on AI's addictive nature

> **"Always check your answers. And no that doesn't mean you get AI to write the code and the tests. Preferably, AI writes neither, and it shows you the way as a glorified combined search engine/rubber duck."**
- Developer on verification

---

## Specific Examples Shared

### Success Stories

1. **Writing specs quickly** - "No one enjoys it" but AI helps with the tedium
2. **ERB template generation** - "Using cursor to generate erb templates helps getting started with the views much faster"
3. **Quick algorithm templates** - "I needed a template depth-first search quickly. The algorithm was correct but ugly."
4. **Research assistance** - Using Claude to analyze user interview transcripts
5. **Building complex features** - "I've been able to build features that would normally take a larger team with deep expertise"

### Failure Stories

1. **Invented methods** - "Invented completely unknown core Ruby methods even after being pressed about where the methods came from"
2. **Config disasters** - "I tried to get it to write a github action, and it couldn't even get the name of the file right"
3. **ActiveSupport assumptions** - "It thinks you use activesupport where you don't. It thinks you are using dry-rb, but you don't"
4. **Migration mishaps** - "A junior dev used Cursor to write a migration, and instead of generating a migration, it created a new file and gave it a bogus timestamp"
5. **Test quality issues** - "Every time I ask for test code it spits out garbage and I rewrite the whole thing"

---

## Insights

### Actionable Advice from Community

1. Start with small, well-defined tasks
2. Always verify and understand the output
3. Use AI for rough drafts, not final code
4. Don't let AI write both code and tests
5. Challenge everything AI suggests
6. Use multiple AI tools to compare results
7. Treat AI as a rubber duck or search engine, not a developer

### Demographics to Consider

- **Experience levels vary widely** - from beginners to 11+ year veterans
- **Role distribution** - Individual contributors, tech leads, principals all represented
- **Strong ethical concerns** - Several respondents cite environmental and labor exploitation issues
- **Tool cost sensitivity** - Concern about becoming dependent on expensive tools

---

## Notable Patterns

### What Works Well
- Simple CRUD operations
- Basic scaffolding and boilerplate
- Documentation generation
- Code explanation and debugging help
- Rubber duck debugging
- Quick prototypes

### What Consistently Fails
- Metaprogramming (1.8/5 rating)
- Modern Ruby syntax
- Rails-specific patterns
- Complex architectural decisions
- Security-sensitive code
- Configuration files

### The Middle Ground
Many developers finding success with:
- AI as a thinking partner, not code generator
- Using AI for tedious tasks while keeping creative work human
- Treating AI output as starting points requiring significant revision
- Multiple AI tools for comparison and validation

---


*Analysis compiled from 34 Ruby developer responses, September 2025*