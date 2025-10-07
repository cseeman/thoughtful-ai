# Documentation Prompts

AI prompts for generating YARD documentation, READMEs, and code comments.

## Overview

Documentation is one of AI's strengths for Ruby projects. AI can generate YARD comments, explain complex code, and create READMEs. Always verify technical accuracy and ensure documentation matches actual behavior.

Community finding: Documentation is a strong use case for AI, particularly for YARD comments and README generation.

## Quick Tips

- Provide the actual code to be documented
- Specify format (YARD, RDoc, plain comments)
- Request examples (usage examples make docs helpful)
- Verify accuracy (AI may hallucinate method signatures)
- Keep it updated (re-generate when code changes)

## What Works and What Doesn't

### Example 1: YARD Documentation

**❌ No Code**
```
Write documentation for my User class
```

Why it fails: No code shown, no format specified, missing context about class purpose.

**✅ Complete Context**
```
Context: Rails 7.1

Generate YARD documentation for this User model:

```ruby
class User < ApplicationRecord
  has_many :posts, dependent: :destroy
  has_many :comments

  validates :email, presence: true, uniqueness: true
  validates :name, presence: true, length: { minimum: 2 }

  scope :confirmed, -> { where.not(confirmed_at: nil) }
  scope :recent, ->(days = 7) { where('created_at >= ?', days.days.ago) }

  def full_name
    "#{first_name} #{last_name}".strip
  end

  def confirmed?
    confirmed_at.present?
  end

  def send_welcome_email
    UserMailer.welcome_email(self).deliver_later
  end
end
```

Requirements:
- Use YARD format
- Document all public methods
- Include @param, @return, @raise tags
- Add examples for complex methods
- Document associations and validations
- Add @note tags for important behavior
```

Why it works: Full code shown, specific format (YARD with tags), clear requirements, Rails context.

Result (partial):
```ruby
# Represents a user in the system
#
# Users can create posts and comments. Must be confirmed via email.
#
# @attr [String] email User's email (unique, required)
# @attr [String] name User's name (required, min 2 chars)
# @attr [DateTime] confirmed_at Email confirmation timestamp
class User < ApplicationRecord
  # @!scope class
  # Returns users who confirmed their email
  # @return [ActiveRecord::Relation<User>] confirmed users
  scope :confirmed, -> { where.not(confirmed_at: nil) }

  # @!scope class
  # Returns users created within last N days
  # @param days [Integer] number of days (default: 7)
  # @return [ActiveRecord::Relation<User>] recent users
  # @example Get users from last 30 days
  #   User.recent(30)
  scope :recent, ->(days = 7) { where('created_at >= ?', days.days.ago) }

  # Returns user's full name
  # @return [String] full name with whitespace stripped
  # @example
  #   user.full_name #=> "Jane Doe"
  def full_name
    "#{first_name} #{last_name}".strip
  end

  # Checks if user confirmed email
  # @return [Boolean] true if confirmed_at is set
  def confirmed?
    confirmed_at.present?
  end

  # Queues welcome email for delivery
  # @return [void]
  # @note Email queued via ActiveJob, not sent immediately
  def send_welcome_email
    UserMailer.welcome_email(self).deliver_later
  end
end
```

### Example 2: Service Object Documentation

**✅ dry-monads Pattern**
```
Context: Rails 7.1, dry-monads

Generate YARD documentation for this service:

```ruby
class OrderProcessingService
  def initialize(order_id, payment_processor: StripeProcessor.new)
    @order_id = order_id
    @payment_processor = payment_processor
  end

  def call
    order = find_order
    return Failure(:order_not_found) unless order

    validate_order(order)
      .bind { |ord| process_payment(ord) }
      .bind { |ord| send_confirmation(ord) }
      .bind { |ord| update_inventory(ord) }
  end

  private

  def find_order
    Order.find_by(id: @order_id)
  end

  def validate_order(order)
    return Failure(:invalid_status) unless order.pending?
    Success(order)
  end

  def process_payment(order)
    result = @payment_processor.charge(order.total_amount)
    result.success? ? Success(order) : Failure(:payment_failed)
  end

  def send_confirmation(order)
    OrderMailer.confirmation_email(order).deliver_later
    Success(order)
  end

  def update_inventory(order)
    order.items.each(&:decrement_stock!)
    Success(order)
  end
end
```

Requirements:
- Document public and private methods
- Explain dry-monads Result pattern
- Include @param and @return with Result types
- Add @example showing success and failure cases
- Document dependencies
```

Why it works: Shows full service logic, specifies dry-monads, both success/failure requested, dependency injection noted.

Result (partial):
```ruby
# Processes an order through payment, confirmation, and inventory update
#
# Uses dry-monads Result pattern. Returns Success(order) if all steps complete,
# or Failure(error_symbol) if any step fails.
#
# @example Successful order
#   service = OrderProcessingService.new(order_id: 123)
#   result = service.call
#   result.success? #=> true
#
# @example Failed payment
#   service = OrderProcessingService.new(order_id: 456)
#   result = service.call
#   result.failure? #=> true
#   result.failure  #=> :payment_failed
class OrderProcessingService
  # Initialize the service
  #
  # @param order_id [Integer] ID of order to process
  # @param payment_processor [#charge] payment processor (default: StripeProcessor)
  def initialize(order_id, payment_processor: StripeProcessor.new)
    @order_id = order_id
    @payment_processor = payment_processor
  end

  # Process the order through all steps
  #
  # Workflow:
  # 1. Find order
  # 2. Validate status and inventory
  # 3. Process payment
  # 4. Send confirmation
  # 5. Update inventory
  #
  # @return [Dry::Monads::Result::Success<Order>] if processing succeeds
  # @return [Dry::Monads::Result::Failure<Symbol>] if any step fails
  #   Possible failure symbols:
  #   - :order_not_found
  #   - :invalid_status
  #   - :payment_failed
  def call
    # ...
  end
end
```

### Example 3: README Generation

**✅ Gem README**
```
Context: Rails 7.1 gem for rate limiting

Generate README for:

Gem name: rack-rate-limiter
Purpose: Rack middleware for rate limiting HTTP requests
Target audience: Rails and Rack developers

Features:
- Configure limits per endpoint
- Multiple storage backends (Redis, Memcached, memory)
- Customizable rate limit headers
- Flexible key generation (IP, user ID, custom)
- Integrates with Rails and Sinatra

Include:
- Installation
- Quick start
- Configuration options
- Rails integration example
- Advanced usage (custom keys)
- License (MIT)
```

Why it works: Clear gem purpose, target audience, feature list, specific sections.

Result (partial):
```markdown
# Rack Rate Limiter

Flexible Rack middleware for rate limiting HTTP requests in Ruby web applications.

## Features

- Configure rate limits per endpoint
- Multiple storage backends (Redis, Memcached, in-memory)
- Standard rate limit headers
- Flexible key generation (IP, user ID, custom)
- Works with Rails, Sinatra, and Rack apps

## Installation

Add to your Gemfile:

```ruby
gem 'rack-rate-limiter'
```

## Quick Start

### Rails Integration

```ruby
# config/application.rb
config.middleware.use Rack::RateLimiter,
  limit: 100,        # requests
  window: 3600,      # per hour
  storage: :redis
```

### Sinatra Integration

```ruby
use Rack::RateLimiter,
  limit: 100,
  window: 3600
```

## Configuration

```ruby
use Rack::RateLimiter,
  limit: 100,
  window: 3600,
  storage: :redis,
  key: ->(req) { req.env['HTTP_X_API_KEY'] || req.ip }
```

## Advanced Usage

### Per-Endpoint Limits

```ruby
use Rack::RateLimiter do |limiter|
  limiter.limit '/api/heavy', limit: 10, window: 60
  limiter.limit '/api/light', limit: 1000, window: 60
  limiter.default limit: 100, window: 60
end
```

## Response Headers

```
HTTP/1.1 429 Too Many Requests
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1642435200
```

## License

MIT License
```

## Community Insights

### What Works
- YARD comments - AI generates accurate parameter and return types
- README generation - Good at standard sections
- Code explanations - Explaining complex code
- Examples - Generating usage examples from code

### What Requires Verification
- Return types - May hallucinate ActiveRecord types
- Exceptions - May miss @raise tags
- Edge cases - Examples may not cover all scenarios
- Version-specific - May suggest deprecated methods

### Pro Tips

> "Always verify method signatures - AI sometimes hallucinates parameters"

> "For READMEs, provide the feature list - AI structures it well"

> "Request examples - documentation without examples is useless"

> "Re-run doc generation when code changes - docs drift quickly"

Key takeaway: Documentation is a great AI use case, but always verify method signatures match actual code, return types are accurate, examples work, and edge cases are covered.

## Prompt Templates

### YARD Documentation
```
Context: Rails [version]

Generate YARD documentation for [class/module/method]:

```ruby
[Code here]
```

Requirements:
- Use YARD format
- Include @param, @return, @raise tags
- Add @example with realistic usage
- Document all public methods
- Add @note for important behavior
```

### README Generation
```
Context: [Type of project]

Generate README for:

Project: [name]
Purpose: [what it does]
Target audience: [who uses it]

Features:
- [feature 1]
- [feature 2]

Include:
- Installation
- Quick start
- Configuration
- Examples

License: [type]
```

### Code Explanation
```
Context: Rails [version]

Explain this code and add inline comments:

```ruby
[Complex code]
```

Explain:
1. Overall purpose
2. Each major step
3. Gotchas or edge cases
4. Why this approach

Audience: [Junior/Intermediate developers]
```

## Related Resources

- [YARD Documentation](https://yardoc.org/)
- [RDoc](https://ruby.github.io/rdoc/)
- [Ruby Style Guide - Comments](https://rubystyle.guide/#comments)

---

Good documentation is maintained documentation. Use AI to bootstrap docs, but keep them updated as code evolves.
