# Refactoring Prompts

AI prompts for improving existing Ruby code while maintaining functionality.

## Overview

Refactoring with AI works best when you're explicit about preserving behavior. The key is showing the current code, specifying exactly what should improve, and what must stay the same.

## Quick Tips

- Preserve functionality ("maintain exact same behavior")
- Show current code (don't just describe it)
- Set specific constraints (line limits, idioms to use)
- Request explanations ("explain each change and why")
- Always run your tests after

## What Works and What Doesn't

Based on community feedback and experience.

### Example 1: Basic Method Refactoring

**❌ Too Vague**
```
Make this code better
```

Why it fails: "Better" is subjective. No constraints, no indication of what to preserve. AI needs explicit guidance about Ruby idioms.

**✅ Specific Goals**
```
Refactor this Ruby method to improve readability while maintaining exact functionality:

```ruby
def get_user_by_id(user_id)
  if user_id != nil
    user = User.where(id: user_id).first
    if user != nil
      return user
    else
      return nil
    end
  else
    return nil
  end
end
```

Requirements:
- Maintain exact same behavior (return user or nil)
- Follow Ruby Style Guide (guard clauses, no explicit returns, no != nil)
- Improve readability (reduce nesting)
- Use idiomatic Ruby patterns (safe navigation, early returns)
- Rename to follow Rails conventions (remove "get_" prefix)
- Add YARD documentation
- Explain each change and why

Context: Rails 7.1 controller helper method
```

Why it works: Specific improvements, behavior preservation explicit, style guidance, explanation request forces AI to justify changes.

Result:
```ruby
# Finds a user by ID
# @param user_id [Integer, nil] the user ID to find
# @return [User, nil] the found user or nil
def find_user(user_id)
  return if user_id.nil?
  User.find_by(id: user_id)
end
```

Changes explained:
1. Removed `get_` prefix (Rails convention)
2. Guard clause for nil check (Ruby Style Guide)
3. Replaced `!= nil` with `.nil?` (Ruby idiom)
4. Used `find_by` instead of `where().first` (Rails idiom)
5. Removed explicit returns (Ruby convention)
6. Reduced nesting from 3 levels to 1

### Example 2: Enumerable Refactoring

**❌ Vague**
```
Refactor this to be more Ruby-like
```

Code:
```ruby
def active_user_emails(users)
  result = []
  users.each do |user|
    if user.active?
      result << user.email
    end
  end
  return result
end
```

Why it fails: AI often struggles with idiomatic enumerable usage. Too vague about what "Ruby-like" means.

**✅ Specific Enumerables**
```
Refactor using idiomatic enumerable methods while maintaining exact functionality:

```ruby
def active_user_emails(users)
  result = []
  users.each do |user|
    if user.active?
      result << user.email
    end
  end
  return result
end
```

Requirements:
- Use Ruby enumerable methods (select, map, filter_map)
- Maximum 3 lines for method body
- No explicit return statements
- No intermediate variables
- Handle nil users array gracefully
- Explain why refactored version is better

Constraints:
- Must return same type (Array of Strings)
- Must preserve order

Context: Mailer helper, Ruby 3.2
```

Why it works: Specific enumerable hints, clear constraints, Ruby version specified (knows filter_map available).

Result:
```ruby
def active_user_emails(users)
  users&.select(&:active?)&.map(&:email) || []
end
```

or (Ruby 2.7+):
```ruby
def active_user_emails(users)
  users&.filter_map { |user| user.email if user.active? } || []
end
```

### Example 3: Metaprogramming (Proceed with Caution)

**⚠️ AI's Weakest Area**
```
Context: Rails 7.1 application

This model has repetitive status checking methods:

```ruby
class Order < ApplicationRecord
  STATUSES = %w[pending processing shipped delivered cancelled].freeze

  def pending?
    status == 'pending'
  end

  def processing?
    status == 'processing'
  end

  def shipped?
    status == 'shipped'
  end

  def delivered?
    status == 'delivered'
  end

  def cancelled?
    status == 'cancelled'
  end
end
```

Refactor using metaprogramming to reduce duplication.

Requirements:
- Use define_method or class_eval
- Maintain exact same public API
- Methods must appear in .methods output
- Add YARD documentation
- Must be readable to junior developers
- Explain trade-offs of metaprogramming approach

WARNING: Metaprogramming is AI's weakest area
Always review metaprogramming code carefully
```

Why this approach helps: Shows existing code, specific technique, readability constraint prevents over-cleverness. Community wisdom: "Let it rough draft, then you refine."

Result (requires careful review):
```ruby
class Order < ApplicationRecord
  STATUSES = %w[pending processing shipped delivered cancelled].freeze

  # Dynamically defines status checking methods
  # @example
  #   order.pending? #=> true if status == 'pending'
  STATUSES.each do |status_name|
    define_method "#{status_name}?" do
      status == status_name
    end
  end
end
```

Trade-offs:
- ✅ DRY, easy to add new statuses
- ❌ Less explicit, harder to debug, no IDE autocomplete
- 💡 Alternative: Consider Rails `enum` for this use case

### Example 4: N+1 Query Refactoring

**✅ Performance Optimization**
```
Context: Rails 7.1, PostgreSQL

This controller action has N+1 query problems:

```ruby
class PostsController < ApplicationController
  def index
    @posts = Post.all

    # In the view, we access:
    # - post.user.name
    # - post.comments.count
    # - post.tags.map(&:name)
  end
end
```

Refactor to eliminate N+1 queries.

Requirements:
- Use eager loading (includes, preload, eager_load)
- Maintain exact same functionality
- Follow Rails conventions
- Explain difference between includes/preload/eager_load
- Show before/after query count

Context: Posts belong_to User, have_many Comments, have_many Tags through PostTags
```

Why it works: Shows actual N+1 code, lists Rails tools, requests explanation, provides association context.

Result:
```ruby
class PostsController < ApplicationController
  def index
    @posts = Post.includes(:user, :comments, :tags).all
  end
end
```

Explanation:
- Query count: Before 3N+1, After 4 queries total
- `includes(:user)` - eager loads user (avoids N+1 for post.user.name)
- `includes(:comments)` - preloads comments for count
- `includes(:tags)` - eager loads tags through join table

When to use each:
- `includes` - Smart choice, uses LEFT OUTER JOIN or separate queries
- `preload` - Separate queries always (use when no filtering on associations)
- `eager_load` - LEFT OUTER JOIN always (use when filtering in WHERE clause)

## Community Insights

### What Works
- Simple code cleanup - Removing explicit returns, fixing indentation
- Rails conventions - Renaming methods, following RESTful patterns
- Basic optimizations - N+1 queries, eager loading
- Style guide compliance - Guard clauses, Ruby idioms

### What Requires Extra Care
- **Metaprogramming** - AI often generates overly complex or incorrect dynamic code
- **Blocks/iterators** - May not use most idiomatic enumerable methods
- **Rails "magic"** - Runtime symbol definitions, DSLs
- **Performance-critical code** - AI doesn't always understand performance implications

### Common AI Mistakes
- Over-engineering - Making code unnecessarily complex
- Breaking behavior - Changing edge case handling
- Non-idiomatic patterns - Using patterns from other languages
- Removing important comments - Losing context about why code exists

### Pro Tips

> "Be explicit about preserving behavior - AI loves to change things"

> "For metaprogramming, let AI draft it, but rewrite it yourself"

> "Always specify 'explain the changes' - helps catch unintended modifications"

> "Test before and after - AI can introduce subtle bugs"

Key takeaway: Refactoring is great for AI, but treat it as a "rough draft":
1. Let AI generate the refactored version
2. Review every change carefully
3. Run your test suite
4. Verify performance hasn't degraded
5. Check for Ruby idiomaticity

The more dynamic and Ruby-specific the code, the more human review needed.

## Prompt Templates

### Basic Refactoring
```
Refactor this Ruby method to improve [readability/performance] while maintaining exact functionality:

[Code here]

Requirements:
- Maintain exact same behavior
- Follow Ruby Style Guide
- [Specific improvements wanted]
- Add YARD documentation
- Explain changes made

Context: [Rails version, purpose]
```

### Enumerable Refactoring
```
Refactor using idiomatic enumerable methods:

[Code here]

Requirements:
- Use [select, map, filter_map, etc.]
- Maximum [N] lines
- No intermediate variables
- Handle nil gracefully
- Explain why better

Context: Ruby [version]
```

### Performance Refactoring
```
Refactor to improve [database/memory] performance:

[Code here]

Current issues:
- [Specific performance problem]

Requirements:
- Optimize [queries/memory usage]
- Follow Rails conventions
- Explain performance improvements

Context: Rails [version], [database]
```

## Related Resources

- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Style Guide](https://rails.rubystyle.guide/)
- [Refactoring: Ruby Edition](https://martinfowler.com/books/refactoringRubyEd.html)

---

Refactoring should improve code quality without changing behavior. Always test thoroughly.
