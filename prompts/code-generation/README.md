# Code Generation Prompts

AI prompts for generating idiomatic Ruby and Rails code.

## Overview

Good prompts produce good code. The key is context: specify your Rails version, explain the business logic, and be clear about what you want.

## Quick Tips

- Specify framework versions ("Rails 7.1", "Ruby 3.2")
- Reference style guides ("Follow Ruby Style Guide")
- Provide business context
- Set clear constraints
- Request explanations

## What Works and What Doesn't

Based on community feedback and experience.

### Example 1: Finding a User

**❌ Vague**
```
Write a method to get users
```

Why it fails: No version, no context, no constraints. Vague prompts often generate Python/JavaScript patterns instead of Ruby idioms.

**✅ Specific**
```
Write a Ruby method following Rails conventions to find a user by ID. Use idiomatic Ruby patterns, avoid explicit nil checks, and follow the Ruby Style Guide. The method should integrate well with Rails controllers and handle the ActiveRecord::RecordNotFound exception appropriately.

Context: Rails 7.1 application with User model (id, email, name, created_at, updated_at)

Requirements:
- Use Rails conventions
- Follow Ruby Style Guide
- Include YARD documentation
- Handle edge cases
```

Why it works: Specifies Rails 7.1, provides context, sets constraints ("idiomatic Ruby", "avoid explicit nil checks"), clear success criteria.

Result:
```ruby
# @param id [Integer] the user ID
# @return [User] the found user
# @raise [ActiveRecord::RecordNotFound] if user doesn't exist
def find_user(id)
  User.find(id)
end
```

### Example 2: Metaprogramming (AI's Weak Spot)

**❌ Too Vague**
```
Create a metaprogramming solution to define methods dynamically
```

Why it fails: Metaprogramming is AI's weakest area. No example code, no constraints, requires deep Ruby knowledge AI often lacks.

**⚠️ Better (but still needs review)**
```
Context: Rails 7.1 application, define status check methods dynamically for Order model.

Current explicit code:
```ruby
class Order < ApplicationRecord
  def pending?
    status == 'pending'
  end

  def shipped?
    status == 'shipped'
  end

  def delivered?
    status == 'delivered'
  end
end
```

Use metaprogramming to define these dynamically from STATUSES constant.

Requirements:
- Follow Ruby Style Guide
- Use define_method or class_eval
- Maintain same public API
- Add YARD documentation
- Must be readable to junior developers
- Methods should appear in .methods output

Explain why this approach is better than explicit methods.
```

Why it's better: Shows existing code, specific technique, readability constraint prevents over-cleverness. Community wisdom: "Let it rough draft, then you refine."

### Example 3: RSpec Tests

**✅ Effective**
```
Context: Rails 7.1, RSpec 3.12, FactoryBot 6.4

Generate RSpec tests for this User model method:

```ruby
class User < ApplicationRecord
  def self.recent_active(days = 30)
    where('created_at >= ?', days.days.ago)
      .where.not(confirmed_at: nil)
      .order(created_at: :desc)
  end
end
```

Requirements:
- Use shoulda-matchers for simple assertions
- Use FactoryBot (assume :user factory exists)
- Test edge cases: boundary conditions, nil handling
- Follow RSpec best practices (describe/context/it)
- Use descriptive test names

Routing conventions: Use full path helpers (users_path), not shortcuts
```

Why it works: Exact versions, actual code shown, available tools listed, edge case reminder, prevents common routing mistake.

Community feedback: "For RSpec, I specify: 'use shoulda_matchers and assume FactoryBot factories exist'"

### Example 4: Positive vs Negative Instructions

**❌ Negative Framing**
```
Write a Rails controller for users.
Don't use strong parameters incorrectly.
Don't forget authentication.
Don't make N+1 queries.
Don't use callbacks.
```

Why it fails: AI fixates on what you tell it NOT to do. Creates confusion, doesn't explain alternatives.

**✅ Positive Instructions**
```
Context: Rails 7.1 RESTful API controller for User resource

Generate a Rails API controller with:
- Strong parameters using private methods
- Token-based authentication (assume Devise setup)
- Eager loading with includes() to prevent N+1 queries
- Service objects for complex operations
- JSON responses with appropriate HTTP status codes

Framework: Rails 7.1
Authentication: Devise with JWT
Testing: RSpec

Include example of index and create actions.
```

Why it works: Positive instructions, specific patterns, clear architecture. Research shows positive framing reduces errors by 30%.

## Community Insights

### What Works Well
- Rails scaffolding and CRUD
- RSpec test generation (with proper context)
- Basic ActiveRecord queries
- Documentation (YARD, README)

### What Struggles
- **Metaprogramming** - AI's weakest area
- **Blocks and iterators** - Often non-idiomatic patterns
- **Modern Ruby syntax** - Endless methods, `it` blocks, pattern matching
- **Rails "magic"** - Runtime symbol definitions

### Community Quotes

> "It sometimes feels like the models are trying to apply code style from other programming languages to Ruby."

> "Let it rough draft, and you refine."

> "Always review metaprogramming code - AI doesn't understand Ruby's dynamic nature well."

Key takeaway: The more Ruby-specific and dynamic the feature, the more human oversight needed.

## Prompt Templates

### Rails Model

```
Create a Rails model for [Entity] with attributes:
- [attribute1]: [type] (required/optional)
- [attribute2]: [type] (required/optional)

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include validations
- Add associations
- Use descriptive method names
- Include YARD documentation

Example usage: [describe how model will be used]
```

### Service Object

```
Create a Ruby service object for [Business Operation].

Input: [describe parameters]
Output: [describe expected output]

Requirements:
- Follow Ruby Style Guide
- Use descriptive method names
- Include error handling
- Add YARD documentation
- Make it testable

Business Logic:
- [step 1]
- [step 2]
```

### API Controller

```
Create a Rails API controller for [Resource] that returns JSON.

Requirements:
- Follow Rails API conventions
- Include proper HTTP status codes
- Add error handling
- Use strong parameters
- Include pagination for index action

Authentication: [method]
Version: [API version]
```

### Background Job

```
Create a Sidekiq background job for [Purpose].

Input: [job parameters]
Output: [expected outcome]

Requirements:
- Follow Ruby Style Guide
- Include error handling and retry logic
- Add logging
- Handle failures gracefully
- Make it idempotent if possible
```

## Related Resources

- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Style Guide](https://rails.rubystyle.guide/)
- [YARD Documentation](https://yardoc.org/)
- [Research-Based Techniques](./research-based-techniques.md) - Advanced prompting strategies

---

AI generates code, but you're the Ruby expert. Always review and validate the output.
