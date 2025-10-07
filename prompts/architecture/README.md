# Architecture Prompts

AI prompts for discussing and designing Rails application architecture.

## Overview

Architecture discussions require deep context. While AI can suggest patterns and explain trade-offs, architectural decisions should be made by humans who understand the business context, team capabilities, and long-term implications.

Community finding: AI can suggest patterns and explain trade-offs, but often struggles with complex architectural decisions. Use AI for brainstorming, not final decisions.

## Quick Tips

- Provide business context (users, scale, team size)
- Specify constraints (timeline, team experience)
- Request trade-offs (pros/cons of approaches)
- Mention existing architecture
- Be skeptical of complexity

## What Works and What Doesn't

### Example 1: Pattern Explanation

**❌ Vague**
```
What's the best Rails architecture?
```

Why it fails: "Best" depends on team, scale, and business needs. No context about application type or size.

**✅ Context-Rich**
```
Context: Rails 7.1 monolith

Current situation:
- Team: 4 Rails developers
- Users: 50,000 active
- Database: PostgreSQL, 100GB
- Deploy: Heroku, single dyno + Sidekiq
- Pain points:
  * Controllers getting fat (200+ lines)
  * Models have too much business logic
  * Hard to test complex workflows

We're considering service objects and form objects.

Questions:
1. Is this premature optimization for our scale?
2. What patterns would you recommend and why?
3. What are the trade-offs?
4. Are there simpler solutions we should try first?

Explain reasoning with Rails-specific examples.
```

Why it works: Team context, scale indicators, specific pain points, proposed solution, open questions invite critical analysis.

AI response will include:
- Analysis of whether patterns fit the scale
- Specific recommendations with examples
- Trade-offs (benefits vs complexity)
- Simpler alternatives to try first
- When to avoid over-engineering

### Example 2: Microservices Decision

**✅ Critical Analysis Request**
```
Context: Rails 7.1 e-commerce app

We're debating extracting payments into a separate microservice.

Current:
- Monolith (~80 models)
- Stripe integration in app/services/payment_service.rb
- 500-1000 payments/day
- 6-person Rails team

Proposal:
- Extract to separate Rails API
- Communicate via REST
- Separate database

Arguments FOR:
- "Isolates payment logic"
- "Can scale independently"
- "Better security isolation"

Arguments AGAINST:
- "Adds operational complexity"
- "Network latency"
- "Team has no microservice experience"

Please analyze:
1. Are we solving a real problem or chasing trends?
2. What questions should we answer first?
3. What simpler alternatives exist?
4. If we extract, what are the gotchas?
```

Why it works: Specific decision, current state clear, scale data, team context, both sides presented, asks AI to challenge the proposal.

AI response:
```
**Short answer: This is likely premature.**

**Analysis:**
- 500-1000 payments/day is NOT high volume
- No indication of payment-related performance issues
- Team has no microservice experience (operational risk)

**Questions to answer first:**
1. What actual problem are you experiencing?
2. Have you tried horizontal scaling?
3. What's your payment error rate?
4. Can you afford the operational overhead?

**Simpler alternatives:**
1. Better organization within monolith (modules/service objects)
2. Async processing with background jobs
3. Read replicas if reads are slow

**When to actually extract:**
- Payments causing main app crashes
- PCI compliance requires isolation
- 10K+ payments/day with documented bottlenecks
- Team has microservice experience
```

### Example 3: Service Object Pattern

**✅ Learning-Focused**
```
Context: Rails 7.1

I keep seeing "service objects" mentioned. Explain:

1. What problem do they solve?
2. When to use vs keeping logic in models/controllers?
3. Show a concrete before/after example
4. What are common mistakes?

My team is comfortable with Rails conventions but hasn't used design patterns beyond MVC.
```

Why it works: Specific pattern, learning-focused, team context, concrete request.

AI response includes:
- Problem service objects solve
- When to use vs not use
- Before/after Rails example
- Common implementation mistakes
- Trade-offs explained

## Community Insights

### What AI Does Well
- Explaining patterns (service objects, form objects, decorators)
- Showing examples (before/after refactorings)
- Listing trade-offs (pros/cons)
- Pattern comparisons (when to use X vs Y)

### What Requires Human Judgment
- Business context (AI doesn't know your users)
- Team capabilities (AI can't assess comfort level)
- Scale decisions (AI tends to over-engineer)
- Political factors (organizational constraints)

### Common AI Pitfalls
- Suggesting microservices too early
- Overcomplicated patterns (clean architecture for simple apps)
- Ignoring team size (patterns needing 20+ devs)
- Theoretical solutions (not Rails-idiomatic)

### Pro Tips

> "Always provide scale numbers - AI needs to know if you're 100 users or 1M users"

> "Ask AI to challenge your assumptions, not just validate them"

> "Request Rails-specific examples, not generic design patterns"

> "Mention your team's experience level"

Key takeaway: AI is a brainstorming partner, not an architect. Use AI to explore options and understand trade-offs, but don't blindly follow suggestions or let AI push you toward complexity.

Remember: "Rails is omakase" - start with conventions, add patterns only when pain is real.

## Prompt Templates

### Pattern Explanation
```
Context: Rails [version]

I want to understand [pattern] in a Rails context.

Explain:
1. What problem does this solve in Rails?
2. When to use it vs Rails conventions?
3. Show a concrete before/after example
4. Common mistakes?
5. Any Rails gems that help?

My team is comfortable with [experience level].
```

### Architectural Decision Review
```
Context: Rails [version]

Current situation:
- Team: [size and experience]
- Scale: [users, requests, data]
- Current architecture: [describe]
- Pain points: [specific problems]

We're considering: [proposed change]

Arguments for: [list]
Arguments against: [list]

Please analyze:
1. Are we solving a real problem or chasing trends?
2. What questions should we answer first?
3. What simpler alternatives exist?
4. If we proceed, what are the gotchas?

Be critical - challenge our assumptions.
```

### Refactoring Strategy
```
Context: Rails [version]

Current organization:
[Describe structure]

Problems:
- [Problem 1 with evidence]
- [Problem 2 with evidence]

Goals:
- [What we want to improve]

Constraints:
- Team size: [number]
- Timeline: [timeframe]
- Can't afford: [downtime, rewrites, etc.]

What refactoring approach would you recommend?
Suggest incremental steps.
```

## Related Resources

- [Rails Doctrine](https://rubyonrails.org/doctrine)
- [Sustainable Rails](https://sustainable-rails.com/) - David Copeland
- [Growing Rails Applications](https://pragprog.com/titles/d-kegrap/growing-rails-applications-in-practice/)

---

Good architecture emerges from real problems, not trends. Start simple (Rails conventions), add patterns only when pain is clear, and always consider your team's capacity for complexity.
