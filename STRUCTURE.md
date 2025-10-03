# Repository Structure

Detailed breakdown of the `thoughtful-ai-ruby-examples` repository organization.

---

## Directory Layout

```
thoughtful-ai-ruby-examples/
├── prompts/                 # Organized prompt categories
│   ├── code-generation/     # Scaffolding, CRUD, boilerplate
│   ├── refactoring/         # Code improvement and cleanup
│   ├── testing/            # RSpec, test cases, edge cases
│   ├── documentation/      # YARD, README, comments
│   ├── debugging/          # Error analysis, troubleshooting
│   └── architecture/       # Design decisions, patterns
│
├── examples/               # Before/after comparisons
│   ├── before-after/       # Prompt effectiveness examples
│   ├── workflows/          # Complete development workflows
│   └── case-studies/       # Real-world scenarios
│
├── guides/                 # Learning resources
│   ├── getting-started/    # Introduction to AI tools
│   ├── advanced-techniques/ # Sophisticated prompting
│   └── troubleshooting/    # Common pitfalls and solutions
│
├── templates/              # Reusable prompt templates
│   ├── rails/              # Rails-specific templates
│   ├── rspec/              # Testing templates
│   ├── yard/               # Documentation templates
│   └── git/                # Commit message templates
│
└── resources/              # External resources and research
    ├── tools/              # AI tool recommendations
    ├── articles/           # Curated reading list
    ├── research/           # Survey data, NIST framework
    └── community-resources.md  # Comprehensive resource list
```

---

## Key Directories Explained

### `/prompts`

Category-organized prompts for specific Ruby/Rails tasks. Each subdirectory contains:
- `README.md` - Overview and best practices for that category
- Individual `.md` files with specific prompt templates
- Examples showing effective vs. ineffective prompting

**Currently available**:
- `code-generation/` - Model, controller, service, migration prompts
- `testing/` - RSpec test generation (coming soon)
- `refactoring/` - Code improvement prompts (coming soon)
- `documentation/` - YARD and README generation (coming soon)

### `/examples`

Real-world examples demonstrating AI effectiveness:

- `before-after/` - Side-by-side comparisons of prompts and results
- `workflows/` - Complete development workflows using AI
- `case-studies/` - Detailed scenarios from real projects

### `/guides`

Learning resources for Ruby developers:

- `getting-started/` - Introduction to AI tools for Ruby developers
- `advanced-techniques/` - Sophisticated prompting strategies
- `troubleshooting/` - Solutions to common AI issues with Ruby

### `/templates`

Ready-to-use prompt templates you can copy and customize:

- `rails/` - Rails model, controller, migration templates
- `rspec/` - RSpec test templates
- `yard/` - Documentation templates
- `git/` - Commit message templates

### `/resources`

External resources and research:

- `research/` - **Survey analysis**, NIST framework, scientific backing
- `tools/` - AI tool comparisons and recommendations
- `articles/` - Curated reading list
- `community-resources.md` - Comprehensive list from conference talk

---

## Finding What You Need

### "I want to generate Ruby code"
→ Start with [`/prompts/code-generation/`](prompts/code-generation/)

### "I want to see if AI actually works for Ruby"
→ Read the [Survey Analysis](resources/research/survey_analysis_thoughtful_ai.md)

### "I'm new to AI tools"
→ Start with the [Getting Started Guide](guides/getting-started/README.md)

### "I want research-backed techniques"
→ Check [Research-Based Techniques](prompts/code-generation/research-based-techniques.md)

### "I want to understand the NIST framework"
→ Read [NIST Explainable AI](resources/research/nist_explainable_ai_integration.md)

### "I attended the talk and want more resources"
→ See [Community Resources](resources/community-resources.md)

---

## Navigation Tips

1. **Use GitHub's search**: Press `/` to search within the repository
2. **Check README files**: Each directory has a README explaining its contents
3. **Follow the links**: README.md has quick links to key resources
4. **Start with survey**: Understand what works (and doesn't) for Ruby developers

---

Back to [Main README](README.md)
