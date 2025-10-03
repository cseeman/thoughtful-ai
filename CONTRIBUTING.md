# Contributing to Thoughtful AI for the Rubyist

Thank you for your interest in contributing! This repository aims to help Ruby developers use AI tools thoughtfully.

---

## What We're Looking For

### Prompts
- Effective prompts for Ruby/Rails development
- Prompts that produce idiomatic Ruby code
- Templates that work across different AI tools
- Examples showing Ruby-specific context

### Examples
- Before/after comparisons showing prompt effectiveness
- Real-world scenarios with actual results
- Both successes and failures (we learn from both!)
- Clear explanations of what worked and why

### Workflows
- Complete development workflows using AI
- Integration with existing Ruby tooling (RSpec, RuboCop, etc.)
- Team collaboration patterns
- Best practices from production use

### Research & Analysis
- Survey data from Ruby developers
- Performance comparisons of AI tools on Ruby code
- Documentation of Ruby-specific AI challenges
- Scientific research relevant to AI-assisted development

---

## Contribution Guidelines

### Format Requirements

**Prompts should include:**
```markdown
## [Descriptive Title]

**Use Case**: What problem this solves

**Prompt Template**:
\`\`\`
[Your prompt here]
\`\`\`

**Example Output**: (Optional but helpful)

**Notes**:
- What works well
- What to watch out for
- Ruby version considerations
```

**Examples should include:**
```markdown
## [Scenario Title]

**Context**: [Rails version, gems, etc.]

### Ineffective Approach
\`\`\`ruby
# Code or prompt that didn't work
\`\`\`
**Why it failed**: [Explanation]

### Effective Approach
\`\`\`ruby
# Code or prompt that worked
\`\`\`
**Why it worked**: [Explanation]
```

### Code Quality

- All Ruby code examples should follow the [Ruby Style Guide](https://rubystyle.guide/)
- Rails examples should follow [Rails conventions](https://rails.rubystyle.guide/)
- Include Ruby/Rails version when relevant
- Test your prompts before submitting

### Tone & Style

- **Welcoming**: Assume good faith from readers
- **Practical**: Focus on real-world usage
- **Honest**: Include both successes and failures
- **Balanced**: Acknowledge AI limitations while showing benefits
- **Human-written**: Avoid AI-generated fluff or excessive emojis

### What NOT to Contribute

- Prompts that generate non-idiomatic Ruby
- Examples without context or explanation
- Marketing content for specific AI tools
- Unverified claims about AI capabilities
- AI-generated content without human review and editing

---

## How to Contribute

### 1. Fork & Branch
```bash
git clone https://github.com/your-username/thoughtful-ai-ruby-examples.git
cd thoughtful-ai-ruby-examples
git checkout -b your-contribution-name
```

### 2. Make Your Changes

Add your contribution in the appropriate directory:
- Prompts → `/prompts/[category]/`
- Examples → `/examples/before-after/`
- Workflows → `/examples/workflows/`
- Research → `/resources/research/`

### 3. Test Your Contribution

- Verify prompts work with at least one AI tool
- Check Ruby code runs and follows style guides
- Ensure links work and formatting is correct
- Review for typos and clarity

### 4. Submit a Pull Request

**PR Title**: Clear, descriptive summary

**PR Description should include**:
- What you're adding
- Why it's useful for Ruby developers
- Which AI tools you tested with (if applicable)
- Any caveats or limitations

### 5. Respond to Feedback

Maintainers may request changes. This is normal and helps maintain quality.

---

## Questions?

- Check existing issues on GitHub
- Review the [survey analysis](resources/research/survey_analysis_thoughtful_ai.md) for community context
- Read the [README](README.md) for project goals

---

## Code of Conduct

### Be Respectful
- Treat all contributors with respect
- Assume good intentions
- Provide constructive feedback
- Welcome newcomers

### Be Honest
- Share both successes and failures
- Acknowledge when you're unsure
- Cite sources when using others' work
- Don't make unverified claims

### Be Thoughtful
- Consider impact on junior developers
- Think about maintainability
- Value code quality over quantity
- Preserve Ruby's human-centered philosophy

---

Thank you for helping make AI more thoughtful for the Ruby community!
