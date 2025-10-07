# AI Prompts for Ruby Developers

Proven prompts that help you work effectively with AI while maintaining idiomatic Ruby code.

## 📚 What's Here

Each guide includes real examples showing what works and what doesn't, based on a survey of 42 Ruby developers.

### [Code Generation](./code-generation/)
Generate Rails models, controllers, services, and background jobs. Learn why metaprogramming (rated 2.1/5) needs extra care, and how to get idiomatic Ruby instead of Python-style code.

**Start here if**: You're writing new code or need Rails scaffolding

### [Testing](./testing/)
Create RSpec tests for models, controllers, and services. Avoid common pitfalls like outdated routing syntax (`get :index` vs `get users_path`).

**Start here if**: You're adding test coverage or practicing TDD

### [Refactoring](./refactoring/)
Improve existing code while preserving behavior. Includes N+1 query fixes, enumerable refactoring, and metaprogramming warnings.

**Start here if**: You're cleaning up legacy code or improving performance

### [Debugging](./debugging/)
Debug with complete error context and focused code extracts. AI excels at explaining stack traces and identifying common Rails errors.

**Start here if**: You're stuck on an error or investigating unexpected behavior

### [Architecture](./architecture/)
Discuss patterns and architectural decisions. AI can explain service objects and trade-offs, but humans make the final call.

**Start here if**: You're considering new patterns or evaluating architectural changes

### [Documentation](./documentation/)
Generate YARD comments, READMEs, and code explanations. Great for bootstrapping docs, but always verify accuracy.

**Start here if**: You're documenting existing code or creating project READMEs

## 💡 Quick Tips

The best prompts include:
- **Versions**: "Rails 7.1", "Ruby 3.2", "RSpec 3.12"
- **Context**: Business logic, team size, existing patterns
- **Constraints**: What must stay the same, what should improve
- **Examples**: Show existing code when possible

The worst prompts:
- Too vague ("make it better", "fix this")
- No versions specified
- Missing context about what's expected
- Entire file dumps instead of focused extracts

## 🤝 Community Insights

Based on feedback from Ruby developers:

**AI works well for**:
- Rails scaffolding and CRUD
- RSpec test generation
- Documentation (YARD, READMEs)
- Debugging common errors

**AI struggles with**:
- Metaprogramming - AI's weakest area
- Blocks and iterators - Often non-idiomatic
- Modern Ruby syntax (endless methods, pattern matching)
- Rails "magic" (runtime behavior)

Key takeaway: The more dynamic and Ruby-specific the code, the more human oversight needed.

## 🌟 Contributing

Found a prompt that works great? Noticed something that could be clearer? We'd love your input.

**Ways to contribute**:
- Share effective prompts you've discovered
- Submit before/after examples showing real improvements
- Report prompts that didn't work as expected
- Suggest better approaches based on your experience

See [CONTRIBUTING.md](../CONTRIBUTING.md) for details.

## 📖 Advanced Techniques

For deeper prompt engineering strategies with research citations, see:
- [Research-Based Techniques](./code-generation/research-based-techniques.md) - Chain-of-thought, few-shot learning, constraint-based prompting

## 🔗 Related Resources

- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Style Guide](https://rails.rubystyle.guide/)
- [RSpec Documentation](https://rspec.info/)
- [YARD Documentation](https://yardoc.org/)

---

Remember: AI generates code, but you're the Ruby expert. Always review, understand, and validate the output.
