# Thoughtful AI for the Rubyist

A collection of AI prompts, examples, and research for Ruby developers who want to use AI tools with intention and purpose.

---

## Quick Links

### For Ruby Developers
- **[Survey Analysis](resources/research/survey_analysis_thoughtful_ai.md)** - What 42 Ruby developers think about AI tools
- **[Getting Started Guide](guides/getting-started/README.md)** - Introduction to AI tools for Ruby
- **[Code Generation Prompts](prompts/code-generation/README.md)** - Templates for generating Ruby/Rails code
- **[Research-Based Techniques](prompts/code-generation/research-based-techniques.md)** - Evidence-backed prompting strategies

### For Conference Talk Attendees
- **[Community Resources](resources/community-resources.md)** - Tools, articles, and further reading
- **[Survey Analysis](resources/research/survey_analysis_thoughtful_ai.md)** - Full community survey findings
- **[NIST Explainable AI](resources/research/nist_explainable_ai_integration.md)** - Applying NIST principles to Ruby development

---

## What's Here

This repository contains practical resources for Ruby developers using AI coding tools:

**Prompts** - Ready-to-use templates for:
- Code generation (models, controllers, services)
- Testing (RSpec, test cases)
- Refactoring and debugging
- Documentation (YARD, READMEs)

**Examples** - Before/after comparisons showing effective prompting

**Research** - Survey data from 42 Ruby developers and scientific backing

**Guides** - How to use AI tools thoughtfully in Ruby development

---

## Repository Structure

```
prompts/           Organized by task (generation, testing, refactoring)
examples/          Real-world before/after comparisons
guides/            Learning resources and best practices
resources/
  └── research/    Survey analysis, NIST framework, context switching
templates/         Reusable prompt templates
```

Full structure details: [STRUCTURE.md](STRUCTURE.md)

---

## Core Principles

**AI as augmentation, not replacement**
- You remain the Ruby expert
- AI handles boilerplate and initial drafts
- Always verify and understand AI output

**Ruby-first approach**
- Maintain readability and expressiveness
- Follow Ruby idioms and Rails conventions
- Preserve developer happiness

**Research-backed practices**
- Community survey insights (42 developers)
- NIST explainability framework
- Understanding automation bias and context switching costs

---

## AI Tools for Ruby

- **GitHub Copilot** - Code completion, integrated into editors
- **Cursor** - AI-native editor with project context
- **Claude Code** - Terminal-based assistant (used to create this talk)
- **Continue.dev** - Open-source, customizable
- **ChatGPT/Claude** - Code review and analysis

See [tools comparison](resources/tools/README.md) for detailed analysis.

---

## Key Findings from Community Survey

Based on 42 Ruby developer responses:

**Adoption**: 38% daily users, 33% non-users, 19% moderate users

**Ruby-specific challenges**:
- Metaprogramming: 2.1/5 (AI's weakest area)
- Rails conventions: 3.3/5 (moderate)
- Blocks/iterators: 2.5/5 (below average)

**Top use cases**: Code generation, writing tests, debugging, documentation

**Community wisdom**: "Let it rough draft, and you refine" - Always verify AI output

Full analysis: [Survey Results](resources/research/survey_analysis_thoughtful_ai.md)

---

## When to Use (and Not Use) AI

**Works well**:
- Rails scaffolding and CRUD operations
- RSpec test skeletons
- Documentation and comments
- Debugging assistance
- Research and exploration

**Use with caution**:
- Metaprogramming and DSLs (AI struggles significantly)
- Security-sensitive code
- Complex business logic
- Architectural decisions
- Custom Rails patterns

---

## Getting Started

1. Read the [Survey Analysis](resources/research/survey_analysis_thoughtful_ai.md) to understand community experiences
2. Browse [Code Generation Prompts](prompts/code-generation/README.md) for practical templates
3. Check [Research-Based Techniques](prompts/code-generation/research-based-techniques.md) for evidence-backed strategies
4. Try examples from [workflows](examples/workflows/) in your own projects

---

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**What we're looking for**:
- Prompts that work well for Ruby/Rails
- Before/after examples showing effectiveness
- Real-world workflows and case studies
- Tool experiences and recommendations

---

## About

This repository supports the "Thoughtful AI for the Rubyist" conference talk, created to help Ruby developers use AI tools thoughtfully while maintaining Ruby's human-centered philosophy.

**Key message**: AI can enhance Ruby development when guided by Ruby values and your professional expertise. You're the expert—AI is just a tool.

---

*Part of the "Thoughtful AI for the Rubyist" community resource collection*
